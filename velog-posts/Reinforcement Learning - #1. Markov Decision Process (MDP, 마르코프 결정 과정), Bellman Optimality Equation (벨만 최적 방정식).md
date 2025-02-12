<h1 id="reinforcement-learning---1-markov-decision-process-mdp-마르코프-결정-과정-bellman-optimality-equation-벨만-최적-방정식">Reinforcement Learning - #1. Markov Decision Process (MDP, 마르코프 결정 과정), Bellman Optimality Equation (벨만 최적 방정식)</h1>
<p>본 문서는 2022년 서울대학교 수리과학부에서 Ernest K. Ryu 교수님께서 진행하신 Reinforcement Learning 강의 내용을 정리한 것입니다.</p>
<h2 id="1-markov-decision-process-mdp">1. Markov Decision Process (MDP)</h2>
<p>강화학습(RL)은 마르코프 결정 과정(MDP) 내에서 순차적 의사결정을 고려함.</p>
<h3 id="1-1-definition">1-1. Definition</h3>
<ul>
<li><p><strong>시간</strong>: $t = 0,1, \cdots , T$</p>
</li>
<li><p><strong>상태 전이:</strong><br />$
s_t \xrightarrow{\pi} a_t \xrightarrow{p} (r_t, s_{t+1})
$</p>
</li>
<li><p><strong>경로 (Trajectory):</strong><br />$
\tau = (s_0, a_0, r_0, s_1, a_1, r_1, \dots, s_{T-1}, a_{T-1}, r_{T-1}, s_T)
$</p>
</li>
<li><p><strong>상태:</strong> $s_t \in \mathcal{S}$</p>
</li>
<li><p><strong>행동:</strong> $a_t \in \mathcal{A}$</p>
<ul>
<li>일반적으로 가능한 행동의 집합은 $s_t$에 따라 달라질 수 있음: $a_t \in \mathcal{A}(s_t)$</li>
</ul>
</li>
<li><p><strong>보상:</strong> $r_t \in \mathbb{R}$</p>
<ul>
<li>정책을 선택하여 보상의 합을 최대화하는 것이 목표</li>
</ul>
</li>
<li><p><strong>종결 시간:</strong> $T$는 <em>terminal time</em> 혹은 <em>stopping time</em></p>
<ul>
<li>$s_T$가 종결 상태이면 $T$가 종료됨.</li>
<li>$T = \infty$도 가능하며, 만약 종결 상태가 $\mathcal{S}$에 포함되지 않으면 $T = \infty$가 반드시 성립.</li>
</ul>
</li>
<li><p><strong>초기 상태 분포:</strong> $s_0 \sim p_0$ (일반적으로 고정됨)</p>
</li>
<li><p><strong>상태 전이 확률:</strong> 환경이 제공하는 확률 분포 $p(r, s' | s, a)$
$
(r_t, s_{t+1}) \sim p(\cdot, \cdot | s_t, a_t)
$</p>
</li>
<li><p><strong>정리</strong></p>
<ul>
<li>상태 $s_t \in \mathcal{S}$</li>
<li>행동 $a_t \in \mathcal{A}$</li>
<li>보상 $r_t \in \mathbb{R}$</li>
<li>종결 시간 $T$ (종료 상태가 존재하지 않으면 $T = \infty$)</li>
<li>초기 상태 분포 $s_0 \sim p_0$</li>
<li>상태 전이 확률 $p(r, s' | s, a)$ (일반적으로 정확히 알려지지 않음)</li>
</ul>
</li>
</ul>
<h3 id="1-2-특성">1-2. 특성</h3>
<ul>
<li><p>$r_t$ 는 경우에 따라 $(s_t, a_t)$ 의 완전히 결정적인 함수일 수 있음.</p>
</li>
<li><p>$s_{t+1}$ 역시 경우에 따라 $(s_t, a_t)$ 의 완전히 결정적인 함수일 수 있음.</p>
</li>
<li><p><strong>stationary</strong> 동역학을 가정:
$$
(r_t, s_{t+1}) \sim p_t(\cdot, \cdot | s, a)
$$
stationary 가정하에:
$$
p_t(r, s' | s, a) = p(r, s' | s, a)
$$
(즉, 시간에 따라 전이확률 p가 변하지 않는다.)</p>
</li>
<li><p><strong>행동 $a_t$ 는 정책 $\pi$ 에 의해 선택됨</strong> (주어진 상태 $s_t$ 에서).</p>
<ul>
<li><strong>확률적 정책</strong> ($\pi$ 가 stochastic인 경우):
$$
\pi(a | s)
$$
는 확률 분포이며, $a_t \sim \pi(\cdot | s_t)$ 를 따름.</li>
<li><strong>결정적 정책</strong> ($\pi$ 가 deterministic인 경우):
$$
a_t = \pi(s_t)
$$<blockquote>
<ul>
<li>일반적으로 <strong>정책 $\pi$ 는 신경망으로 파라미터화됨</strong>:
$$
\pi = \pi_{\theta}
$$
$\theta$: 신경망의 학습 가능한 파라미터</li>
</ul>
</blockquote>
</li>
</ul>
</li>
<li><p>현재는 <strong>에이전트가 상태 $S_t$ 를 완전히 관찰한다고 가정</strong>하지만, 일반적으로 <strong>부분 관찰 환경(partial observation)</strong> 에서는 다음과 같이 정의 가능:
$$
o_t = \phi(s_t)
$$
여기서 $\phi$ 는 상태 $s_t$ 를 변환하는 함수.</p>
</li>
<li><p>cf.</p>
<ul>
<li>정책(Policy)은 비정지(non-stationary)일 수도 있음.</li>
<li>TODO: 종결 상태(Terminal State)에서의 정책 정의 필요.</li>
</ul>
</li>
</ul>
<h2 id="2-강화학습의-목표">2. 강화학습의 목표</h2>
<p>강화학습의 목표는 <strong>기대 할인 반환(Expected Discounted Return)을 극대화하는 것</strong>입니다.</p>
<p>$$
\max_{\pi} J(\pi) = \mathbb{E}^{\pi}<em>{s_0 \sim p_0} \left[ \sum</em>{t=0}^{T-1} \gamma^t r_t \right].
$$</p>
<ul>
<li><p><strong>누적 할인 보상(Cumulative Discounted Return):</strong>
$$
\sum_{t=0}^{T-1} \gamma^t r_t = r_0 + \gamma r_1 + \cdots + \gamma^{T-1} r_{T-1} = G_0.
$$</p>
</li>
<li><p><strong>정의:</strong></p>
<ul>
<li>$G_0$: 누적 반환(Cumulative Return).</li>
<li>$r_t$: 순간 보상(Instantaneous Reward).</li>
<li>할인 계수(Discount Factor): $\gamma \in (0,1]$.</li>
<li>$T = \infty$인 경우, 반환이 유한하게 유지되려면 $\gamma &lt; 1$이어야 함.</li>
<li>$\mathbb{E}^{\pi}$: 정책 $\pi$ 하에서의 기대값.<ul>
<li>$a_t \sim \pi(\cdot | s_t)$</li>
<li>$(r_t, s_{t+1}) \sim p(\cdot, \cdot | s_t, a_t)$</li>
</ul>
</li>
</ul>
</li>
<li><p><strong>시간 $t$부터의 반환(Return from time $t$):</strong>
$$
G_t = r_t + \gamma r_{t+1} + \cdots + \gamma^{T-1-t} r_{T-1} = \sum_{t' = t}^{T-1} \gamma^{t'-t} r_{t'}.
$$</p>
</li>
</ul>
<h2 id="3-상태-가치-함수-vpi-및-상태-행동-가치-함수-qpi">3. 상태 가치 함수 $V^{\pi}$ 및 상태-행동 가치 함수 $Q^{\pi}$</h2>
<h3 id="3-1-상태-가치-함수-state-value-function">3-1. 상태 가치 함수 (State Value Function)</h3>
<p>상태 가치 함수 $V^{\pi}(s)$는 <strong>정책 $\pi$를 따를 때 상태 $s$에서 시작하여 기대되는 반환(Expected Return)</strong>을 의미합니다.</p>
<p>$$
V^{\pi}(s) = \mathbb{E}^{\pi} [G_0 | s_0 = s]
$$</p>
<p>즉, 주어진 상태 $s$에서 정책 $\pi$를 따른 경우 기대되는 보상의 총합입니다.</p>
<h3 id="3-2-상태-행동-가치-함수-state-action-value-function">3-2. 상태-행동 가치 함수 (State-Action Value Function)</h3>
<p>상태-행동 가치 함수 $Q^{\pi}(s, a)$는 <strong>정책 $\pi$를 따를 때 상태 $s$에서 행동 $a$를 수행한 이후 기대되는 반환</strong>을 의미합니다.</p>
<p>$$
Q^{\pi}(s, a) = \mathbb{E}^{\pi} [G_0 | s_0 = s, a_0 = a]
$$</p>
<p>즉, 상태 $s$에서 특정 행동 $a$를 선택했을 때, 그 이후 정책 $\pi$를 따랐을 경우 기대되는 보상의 총합입니다.</p>
<h3 id="3-3-가치-함수의-기본-성질">3-3. 가치 함수의 기본 성질</h3>
<p>정책 $\pi$ 하에서 상태 가치 함수는 상태-행동 가치 함수의 기대값으로 표현될 수 있습니다:</p>
<p>$$
V^{\pi}(s_0) = \mathbb{E}_{a_0 \sim \pi(\cdot | s_0)} [Q^{\pi}(s_0, a_0)]
$$</p>
<p>이는 상태 가치 함수가 <strong>정책 $\pi$에 따라 행동을 선택하는 확률적 기대값</strong>으로 나타낼 수 있음을 의미합니다.</p>
<p>또한, 정지성(stationarity)을 가정하면 다음이 성립합니다:</p>
<p>$$
V^{\pi}(s) = \mathbb{E}^{\pi} [G_t | s_t = s]
$$</p>
<p>$$
Q^{\pi}(s, a) = \mathbb{E}^{\pi} [G_t | s_t = s, a_t = a]
$$</p>
<p>정지성(stationarity)은 상태 가치 함수가 특정 시간 $t$에서 동일한 기대값을 가지는 것이 아니라, 환경의 확률적 동역학이 시간에 따라 변하지 않음을 의미합니다.
즉, 특정 시간 $t$에서의 기대 반환도 동일한 관계를 따르지만, $V(s_0)$와 $V(s_t)$가 같다는 의미는 아닙니다.</p>
<h2 id="4-1-스텝-전이-속성-1-step-transition-property">4. 1-스텝 전이 속성 (1-step Transition Property)</h2>
<h3 id="4-1-상태-가치-함수의-1-스텝-관계">4-1. 상태 가치 함수의 1-스텝 관계</h3>
<p>마르코프 성질에 의해 상태 가치 함수는 다음과 같은 재귀 관계를 가집니다:</p>
<p>$$
V^{\pi}(s) = \mathbb{E}^{\pi} [r_0 + \gamma V^{\pi}(s_1) | s_0 = s].
$$</p>
<p>이를 전개하면:</p>
<p>$$
V^{\pi}(s) = \mathbb{E}^{\pi} \left[ r_0 + \gamma \sum_{t=1}^{T-1} \gamma^{t-1} r_t | s_0 = s \right]
$$</p>
<p>이를 상태-행동 관계로 확장하면:</p>
<p>$$
V^{\pi}(s) = \mathbb{E}_{a_0 \sim \pi(\cdot | s)} \left[ \mathbb{E}^{\pi} \left[ r_0 + \gamma G_1 | s_0 = s, a_0 \right] \right]
$$</p>
<p>이를 정리하면:</p>
<p>$$
V^{\pi}(s) = \mathbb{E}_{a_0 \sim \pi(\cdot | s)} \left[ r_0 + \gamma \mathbb{E}^{\pi} [G_1 | s_1] \right]
$$</p>
<p>$$
= \mathbb{E}_{a_0 \sim \pi(\cdot | s)} \left[ r_0 + \gamma V^{\pi}(s_1) \right].
$$</p>
<h3 id="4-2-상태-행동-가치-함수의-1-스텝-관계">4-2. 상태-행동 가치 함수의 1-스텝 관계</h3>
<p>$$
Q^{\pi}(s, a) = \mathbb{E}^{\pi} [r + \gamma Q^{\pi}(s', a') | s, a]
$$</p>
<p>이를 마르코프 성질을 적용하여 전개하면:</p>
<p>$$
Q^{\pi}(s, a) = \mathbb{E}^{\pi} [r_0 + \gamma G_1 | s_0 = s, a_0 = a]
$$</p>
<p>이를 상태 전이 확률과 행동 선택 확률을 적용하여 풀어 쓰면:</p>
<p>$$
Q^{\pi}(s, a) = \mathbb{E}<em>{(r_0, s_1) \sim p(\cdot | s, a)} \left[ r_0 + \gamma \mathbb{E}</em>{a_1 \sim \pi(\cdot | s_1)} [Q^{\pi}(s_1, a_1)] \right].
$$</p>
<p>즉, <strong>상태-행동 가치 함수는 보상과 할인된 다음 상태의 기대값으로 표현</strong>될 수 있으며, 이는 가치 반복(Value Iteration) 및 Q-러닝(Q-Learning)의 핵심 개념이 됩니다.</p>
<h3 id="4-3-요약">4-3. 요약</h3>
<ol>
<li><strong>$V^{\pi}(s)$</strong>: 특정 상태 $s$에서 시작하여 정책 $\pi$를 따를 때 기대되는 반환.</li>
<li><strong>$Q^{\pi}(s, a)$</strong>: 상태 $s$에서 행동 $a$를 선택하고 이후 정책 $\pi$를 따를 때 기대되는 반환.</li>
<li><strong>벨만 방정식(Bellman Equation)</strong>:<ul>
<li>$V^{\pi}(s)$는 상태 전이 확률과 행동 선택 정책을 반영한 기대값으로 표현 가능.</li>
<li>$Q^{\pi}(s, a)$는 보상과 다음 상태-행동 쌍의 가치 함수의 기대값으로 재귀적으로 표현 가능.</li>
</ul>
</li>
</ol>
<p>이러한 관계들은 <strong>정책 평가(Policy Evaluation), 정책 개선(Policy Improvement), 그리고 최적 정책 학습(Optimal Policy Learning)</strong>에 핵심적으로 사용됩니다.</p>
<hr />
<h2 id="5--바나흐-고정점-정리-banach-fixed-point-theorem">5.  바나흐 고정점 정리 (Banach Fixed Point Theorem)</h2>
<p>바나흐 고정점 정리는 수축 사상(contraction mapping)에 대해 유일한 고정점이 존재함을 보장하는 정리입니다.</p>
<p><strong>정리:</strong></p>
<ul>
<li><p>$\mathcal{X}$가 거리 공간(metric space)이고 거리 함수 $d$를 가진다고 가정합니다.</p>
</li>
<li><p>함수 $\mathcal{T}: \mathcal{X} \to \mathcal{X}$가 <strong>$\gamma$-수축(contraction mapping)</strong>이라면:</p>
<p>$$
d(\mathcal{T}(x), \mathcal{T}(y)) \leq \gamma d(x,y), \quad \forall x,y \in \mathcal{X}, , 0 \leq \gamma &lt; 1
$$</p>
<ul>
<li>이때, $\mathcal{T}$는 고정점을 가지며, 고정점은 유일함.</li>
<li>초기값 $x_0 \in \mathcal{X}$에 대해 $k \to \infty$로 보낼 때, $\mathcal{T}^k(x_0)$는 유일한 고정점 $x^*$로 수렴함:</li>
</ul>
<p>$$
\mathcal{T}^k(x) \to x^*
$$</p>
<ul>
<li>여기서 $x^<em>$는 $\mathcal{T}(x^</em>) = x^*$를 만족하는 유일한 고정점.</li>
</ul>
</li>
</ul>
<h2 id="6-벨만-방정식과-바나흐-정리">6. 벨만 방정식과 바나흐 정리</h2>
<h3 id="6-1-벨만-방정식-bellman-equation-for-vpi">6-1. 벨만 방정식 (Bellman Equation) for $V^{\pi}$</h3>
<h4 id="6-1-1-벨만-방정식의-정의">6-1-1. 벨만 방정식의 정의</h4>
<p>벨만 방정식(Bellman Equation)은 동적 계획법에서 핵심이 되는 방정식으로, <strong>현재 상태에서의 최적 정책이 다음 상태에서도 유지됨을 보장하는 재귀적 관계식</strong>입니다. 이는 가치 함수(value function)를 표현하는 방식으로 사용됩니다.</p>
<p>정책 $\pi$가 주어졌을 때, 상태 가치 함수 $V^{\pi}(s)$는 다음과 같은 관계를 만족합니다:</p>
<p>$$
V^{\pi}(s) = \mathbb{E}<em>{a \sim \pi(\cdot | s)} \left[ \mathbb{E}</em>{(r,s') \sim p(\cdot | s,a)} \left[ r + \gamma V^{\pi}(s') \right] \right]
$$</p>
<p>즉, 상태 $s$에서 정책 $\pi$에 따라 행동을 선택했을 때, 현재 받을 보상과 다음 상태에서 받을 보상의 할인된 합이 기대값으로 나타납니다.</p>
<h3 id="6-2-벨만-연산자bellman-operator와의-관계">6-2. 벨만 연산자(Bellman Operator)와의 관계</h3>
<p>벨만 연산자 $\mathcal{B}^{\pi}$는 벨만 방정식을 보다 쉽게 표현하기 위해 정의된 <strong>연산자(operator)</strong>입니다. 이는 가치 함수 공간에서 가치 함수 공간으로 매핑하는 연산자로 볼 수 있습니다.</p>
<p>$$
(\mathcal{B}^{\pi} V)(s) = \mathbb{E}<em>{a \sim \pi(\cdot | s)} \left[ \mathbb{E}</em>{(r,s') \sim p(\cdot | s,a)} \left[ r + \gamma V(s') \right] \right]
$$</p>
<p>이 연산자는 가치 함수 $V$를 사용하여 다음 상태에서의 기대 가치를 업데이트하는 역할을 합니다. </p>
<p>벨만 방정식은 <strong>$V^{\pi}$가 벨만 연산자의 고정점(fixed point)이 됨을 의미합니다</strong>:</p>
<p>$$
\mathcal{B}^{\pi} V^{\pi} = V^{\pi}
$$</p>
<p>즉, $V^{\pi}$는 벨만 연산자를 적용해도 변하지 않는 상태로 수렴합니다.</p>
<h3 id="6-3-벨만-연산자의-수축성-banach-fixed-point-theorem-적용">6-3. 벨만 연산자의 수축성 (Banach Fixed Point Theorem 적용)</h3>
<p>벨만 연산자가 수축 사상(contraction mapping)임을 보이려면, 두 가치 함수 $V_1$과 $V_2$에 대해 다음이 성립해야 합니다:</p>
<p>$$
| \mathcal{B}^{\pi} V_1 - \mathcal{B}^{\pi} V_2 |<em>{\infty} \leq \gamma | V_1 - V_2 |</em>{\infty}
$$</p>
<p>즉, 벨만 연산자는 항상 입력 간의 거리를 $\gamma$배 축소시키므로 바나흐 고정점 정리에 의해 <strong>$V^{\pi}$는 유일한 해로 수렴</strong>하게 됩니다.</p>
<h3 id="6-4-벨만-방정식-bellman-equation-for-qpi">6-4. 벨만 방정식 (Bellman Equation) for $Q^{\pi}$</h3>
<p>상태-행동 가치 함수(state-action value function) $Q^{\pi}$는 다음을 만족합니다:</p>
<p>$$
Q^{\pi}(s, a) = \mathbb{E}<em>{(r, s') \sim p(\cdot | s, a)} \left[ r + \gamma \mathbb{E}</em>{a' \sim \pi(\cdot | s')} [Q^{\pi}(s', a')] \right]
$$</p>
<p>이는 특정 상태 $s$에서 특정 행동 $a$를 수행한 후, 정책 $\pi$를 계속 따랐을 때의 기대 반환을 의미합니다.</p>
<p>이를 벨만 연산자로 나타내면:</p>
<p>$$
(\mathcal{B}^{\pi} Q)(s, a) = \mathbb{E}<em>{(r, s') \sim p(\cdot | s, a)} \left[ r + \gamma \mathbb{E}</em>{a' \sim \pi(\cdot | s')} [Q(s', a')] \right]
$$</p>
<p>이제, $Q^{\pi}$ 역시 벨만 연산자의 고정점으로 수렴하게 됩니다:</p>
<p>$$
\mathcal{B}^{\pi} Q^{\pi} = Q^{\pi}
$$</p>
<h3 id="6-5-요약">6-5. 요약</h3>
<ol>
<li>벨만 방정식은 가치 함수가 현재 보상과 다음 상태에서의 기대 가치의 합으로 표현되는 재귀적 관계식입니다.</li>
<li>벨만 연산자는 가치 함수를 업데이트하는 연산자로, 벨만 방정식을 더욱 간결하게 표현할 수 있도록 도와줍니다.</li>
<li>벨만 연산자는 $\gamma$-수축 사상이며, 바나흐 고정점 정리에 의해 $V^{\pi}$와 $Q^{\pi}$가 유일한 값으로 수렴함이 보장됩니다.</li>
</ol>
<p>이러한 개념들은 강화학습 알고리즘에서 <strong>정책 평가(Policy Evaluation), 정책 개선(Policy Improvement), 그리고 최적 정책 학습(Optimal Policy Learning)</strong>의 이론적 근거가 됩니다.</p>
<h2 id="7-최적-정책과-최적-가치-함수-optimal-policy-and-value-functions">7. 최적 정책과 최적 가치 함수 (Optimal Policy and Value Functions)</h2>
<h3 id="7-1-최적-정책-optimal-policy">7-1. 최적 정책 (Optimal Policy)</h3>
<p>최적 정책 $\pi^*$는 모든 정책 $\pi$에 대해 가치 함수가 최대가 되는 정책입니다:</p>
<p>$$
V^{\pi^*}(s) \geq V^{\pi}(s), \quad \forall s \in \mathcal{S}, \forall \pi
$$</p>
<p>즉, 최적 정책 $\pi^*$를 따르면 어떤 상태에서도 최대 기대 보상을 받을 수 있습니다.</p>
<ul>
<li><strong>최적 상태 가치 함수</strong>:
$$
V^* = V^{\pi^*}
$$</li>
<li><strong>최적 상태-행동 가치 함수</strong>:
$$
Q^* = Q^{\pi^*}
$$</li>
</ul>
<p>최적 정책 $\pi^<em>$는 유일하지 않을 수 있지만, 최적 가치 함수 $V^</em>$와 $Q^*$는 유일합니다.</p>
<h3 id="7-2-벨만-최적-방정식-bellman-optimality-equation-for-v">7-2. 벨만 최적 방정식 (Bellman Optimality Equation for $V^*$)</h3>
<h4 id="7-2-1-정의">7-2-1. 정의</h4>
<p>최적 상태 가치 함수 $V^*$는 다음의 벨만 최적 방정식을 만족합니다:</p>
<p>$$
V^<em>(s) = \max_{a \in \mathcal{A}} \mathbb{E}_{(r,s') \sim p(\cdot | s,a)} \left[ r + \gamma V^</em>(s') \right]
$$</p>
<p>즉, 상태 $s$에서 가능한 모든 행동 중 최적의 행동을 선택했을 때 얻을 수 있는 최대 기대 반환입니다.</p>
<ul>
<li><strong>최적 정책 $\pi^*$는 다음과 같이 결정됨:</strong>
$$
\pi^<em>(s) = \arg\max_{a \in \mathcal{A}} \mathbb{E}_{(r,s') \sim p(\cdot | s,a)} \left[ r + \gamma V^</em>(s') \right]
$$
이는 최적 상태-행동 가치 함수와도 연결됩니다:
$$
\pi^<em>(s) = \arg\max_{a \in \mathcal{A}} Q^</em>(s,a)
$$</li>
</ul>
<h3 id="7-3-벨만-최적-연산자와-수렴성-bellman-optimality-operator">7-3. 벨만 최적 연산자와 수렴성 (Bellman Optimality Operator)</h3>
<p>벨만 최적 연산자 $\mathcal{B}^*$를 정의하면 다음과 같습니다:</p>
<p>$$
(\mathcal{B}^* V)(s) = \max_{a \in \mathcal{A}} \mathbb{E}_{(r,s') \sim p(\cdot | s,a)} \left[ r + \gamma V(s') \right]
$$</p>
<p>이는 상태 가치 함수의 최적 업데이트 규칙을 나타냅니다.</p>
<ul>
<li>$\mathcal{B}^<em>$가 $\gamma$-수축 사상임을 보일 수 있음:
$$
| \mathcal{B}^</em> V_1 - \mathcal{B}^* V_2 |<em>{\infty} \leq \gamma | V_1 - V_2 |</em>{\infty}
$$
따라서 바나흐 고정점 정리에 의해 $V^*$는 유일한 해로 수렴합니다.</li>
</ul>
<h3 id="7-4-벨만-최적-방정식-bellman-optimality-equation-for-q">7-4. 벨만 최적 방정식 (Bellman Optimality Equation for $Q^*$)</h3>
<p>최적 상태-행동 가치 함수 $Q^*$는 다음의 벨만 최적 방정식을 만족합니다:</p>
<p>$$
Q^<em>(s, a) = \mathbb{E}<em>{(r, s') \sim p(\cdot | s, a)} \left[ r + \gamma \max</em>{a' \in \mathcal{A}} Q^</em>(s', a') \right]
$$</p>
<p>이는 최적 행동을 선택했을 때 기대할 수 있는 최대 보상을 나타냅니다.</p>
<p>최적 정책은 $Q^*$를 기반으로 결정됩니다:</p>
<p>$$
\pi^<em>(s) = \arg\max_{a \in \mathcal{A}} Q^</em>(s,a)
$$</p>
<p>이를 벨만 최적 연산자로 표현하면:</p>
<p>$$
(\mathcal{B}^* Q)(s,a) = \mathbb{E}<em>{(r, s') \sim p(\cdot | s,a)} \left[ r + \gamma \max</em>{a' \in \mathcal{A}} Q(s', a') \right]
$$</p>
<p>이는 가치 반복(Value Iteration) 알고리즘의 핵심 원리입니다.</p>
<h3 id="7-5-벨만-최적-방정식의-적용-조건">7-5. 벨만 최적 방정식의 적용 조건</h3>
<p>최적 가치 함수와 정책이 존재하고 유일한 해로 수렴하려면 다음 조건들이 필요합니다:</p>
<ol>
<li><strong>할인율 조건</strong>: $\gamma \in (0,1)$이어야 함. 만약 $\gamma = 1$이면 보상이 무한대로 발산할 가능성이 있음.</li>
<li><strong>유한한 상태와 행동 공간</strong>: $|\mathcal{S}| &lt; \infty$ 또는 $|\mathcal{A}| &lt; \infty$일 경우 유한한 해가 보장됨.</li>
<li><strong>보상 조건</strong>: 보상 함수 $r$이 유한한 상한 $R$을 가질 경우 수렴 보장이 가능함.</li>
<li><strong>확률적 정책 및 환경 모델</strong>: 상태-전이 확률 $p(s' | s,a)$가 주어져야 하고, 상태가 충분히 방문 가능해야 함.</li>
</ol>
<h3 id="7-6-요약">7-6. 요약</h3>
<ol>
<li>최적 정책 $\pi^*$는 모든 정책 중에서 최적의 기대 보상을 제공하는 정책임.</li>
<li>최적 가치 함수 $V^*$는 벨만 최적 방정식을 만족하는 유일한 해임.</li>
<li>최적 상태-행동 가치 함수 $Q^*$ 역시 벨만 최적 방정식을 만족함.</li>
<li>벨만 최적 연산자는 $\gamma$-수축 사상이며, 바나흐 고정점 정리에 의해 $V^<em>$와 $Q^</em>$는 유일한 값으로 수렴함.</li>
<li>최적 정책과 가치 함수의 수렴성을 보장하기 위해서는 $\gamma$, 상태/행동 공간, 보상 구조 등의 특정 조건이 충족되어야 함.</li>
</ol>
<p>이러한 개념들은 <strong>정책 반복(Policy Iteration), 가치 반복(Value Iteration), 그리고 Q-러닝(Q-Learning)과 같은 강화학습 알고리즘의 핵심 원리</strong>가 됩니다.</p>