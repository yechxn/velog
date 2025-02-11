<h1 id="vision-language-models-vlm의-기초">Vision-Language Models (VLM)의 기초</h1>
<ul>
<li>본 문서는 2024년 서울대학교 수리과학부에서 Ernest K. Ryu 교수님께서 진행하신 <strong>Vision Language Models (VLM)</strong> (Generative AI and Foundation Models - Spring 2024) 강의 내용을 정리한 것입니다. </li>
</ul>
<h2 id="1-clip-contrastive-language-image-pretraining">1. CLIP (Contrastive Language-Image Pretraining)</h2>
<p><img alt="" src="https://velog.velcdn.com/images/yechxn/post/49cb8ba2-3bb4-4fa5-bc90-e258739a3e0b/image.png" /></p>
<p>CLIP 모델은 이미지-캡션 쌍 $(X_i, C_i)$을 이용하여 훈련됩니다.</p>
<ul>
<li><p>이미지 인코더: $f_{\theta}: \mathcal{X} \to \mathbb{R}^d$</p>
</li>
<li><p>텍스트 인코더: $g_{\phi}: \mathcal{C} \to \mathbb{R}^d$</p>
<ul>
<li>목적함수:</li>
</ul>
<p>$$
f_{\theta}(X) \cdot g_{\phi}(C) &gt; 0 \quad \text{(X와 C가 연관될 때)}
$$
$$
f_{\theta}(X) \cdot g_{\phi}(C) &lt; 0 \quad \text{(X와 C가 무관할 때)}
$$</p>
</li>
</ul>
<p>(cf. $\mathbb{R}^d$: 잠재공간)</p>
<h3 id="11-infonce-손실-함수">1.1 InfoNCE 손실 함수</h3>
<p>InfoNCE (Noise Contrastive Estimation) 손실 함수는 다음과 같이 정의됩니다:</p>
<p>$$
\mathcal{L}<em>{NCE} = - \frac{1}{N} \sum</em>{i=1}^N \log \frac{e^{f(X_i, Y_i)}}{\frac{1}{N} \sum_{j=1}^N e^{f(X_i, Y_j)}}
$$</p>
<p>손실 함수는 다음과 같은 방식으로 해석할 수 있습니다:</p>
<ul>
<li><p><strong>분자</strong> $e^{f(X_i, Y_i)}$: $i$-번째 데이터 쌍 $(X_i, Y_i)$가 서로 연관될 때의 유사도 점수를 나타냄.</p>
</li>
<li><p><strong>분모</strong> $\frac{1}{N} \sum_{j=1}^N e^{f(X_i, Y_j)}$: $X_i$와 모든 $Y_j$ (정답 및 오답 포함)의 유사도 점수 합의 평균.</p>
<ul>
<li>이 함수는 기준 샘플 $i$에 대해 정답 쌍 $(X_i, Y_i)$의 유사도를 최대화하고, 다른 샘플 $Y_j$와의 유사도를 최소화하도록 학습</li>
</ul>
</li>
<li><p>f: 유사도 예시</p>
<ul>
<li>$f(X, Y) = X \cdot Y$</li>
<li>$f(X, Y) = \frac{X \cdot Y}{|X| |Y|}$</li>
<li>$f(X, Y) = \log \frac{p(X, Y)}{p_X(X)p_Y(Y)} + \text{constant}$</li>
</ul>
</li>
</ul>
<h3 id="111-infonce의-간소화된-정의">1.1.1 InfoNCE의 간소화된 정의</h3>
<p>InfoNCE 손실은 다음과 같이 간소화될 수 있습니다:</p>
<p>$$
\mathcal{L}<em>{NCE} = \sum</em>{i=1}^N \log \frac{e^{f(X_i, Y_i)}}{\sum_{j=1}^N e^{f(X_i, Y_j)}}
$$</p>
<ul>
<li>이는 상수 계수 $\frac{1}{N}$ 및 상수 항 $\log N$ 만큼의 차이를 제외하면 동일한 손실 함수</li>
</ul>
<h3 id="112-infonce의-역할">1.1.2 InfoNCE의 역할</h3>
<ul>
<li><strong>기준 샘플</strong> $i$: 학습 중 현재 선택된 데이터 샘플.</li>
<li><strong>비교 대상 샘플</strong> $j$: 전체 데이터셋에서 모든 샘플을 포함 (정답 쌍 $j = i$ 및 오답 쌍 $j \neq i$).</li>
<li>손실 함수는 모델이 정답 쌍 ((X_i, Y_i))의 유사도를 더 높이고, 오답 쌍 ((X_i, Y_j))의 유사도를 낮추도록 학습을 유도합니다.</li>
</ul>
<h2 id="2-mutual-information-mi와-infonce">2. Mutual Information (MI)와 InfoNCE</h2>
<p>MI는 두 확률변수 $X, Y$의 상호 정보를 나타내며, 다음과 같이 정의됩니다:
$$
I(X;Y) = \int p(x, y) \log \frac{p(x, y)}{p_X(x) p_Y(y)} dx dy
$$</p>
<h3 id="21-mi와-infonce의-관계">2.1 MI와 InfoNCE의 관계</h3>
<p>$$
MI \geq \mathcal{L}_{NCE}
$$</p>
<ul>
<li>이 정리는 <strong>변분 바운드(Variational Bound)</strong>를 이용하여 증명됩니다.</li>
</ul>
<h4 id="211-대략적인-증명-flow-증명은-생략">2.1.1 대략적인 증명 flow (증명은 생략)</h4>
<ol>
<li>$p(x, y)$, $q(x|y)$를 정의</li>
<li><strong>Jensens's inequality</strong>을 적용하여 바운드를 얻음</li>
<li>$$\log x \leq x/e$$를 활용하여 추가적인 근사</li>
</ol>
<h3 id="22-최적화">2.2 최적화</h3>
<blockquote>
<p>Theorem
$$
\mathcal{L}_{NCE} \to I(X; Y) \quad\text{as } N \to \infty
$$
즉, $N$이 충분히 크면 InfoNCE 손실 함수를 통해 mutual information을 정확히 근사할 수 있음</p>
</blockquote>
<p><strong>[Proof]</strong>
$$
\text{Let } f_<em>(x, y) = \log \frac{p(x, y)}{p_X(x)p_Y(y)} + \text{constant}
$$
$$\text{WTS: }\mathcal{L}<em>{NCE} \to I(X; Y) \quad \text{as } N \to \infty
$$
$$
\mathcal{L}</em>{NCE} = \frac{1}{N} \sum_{i=1}^N \log \frac{e^{f_</em>(X_i, Y_i)}}{\frac{1}{N} \sum_{j=1}^N e^{f_*(X_i, Y_j)}}
$$</p>
<ul>
<li>분모를 따로 계산하면, 
$$
\frac{1}{N} \sum_{j=1}^N e^{f_*(X_i, Y_j)} = e^{\text{constant}} \frac{1}{N} \sum_{j=1}^N \frac{p(X_i, Y_j)}{p_X(X_i)p_Y(Y_j)}
$$
$$=e^{\text{constant}} \left(\frac{1}{N} \frac{p(X_i, Y_i)}{p_X(X_i)p_Y(Y_i)} + \frac{1}{N} \sum_{j \neq i} \frac{p(X_i, Y_j)}{p_X(X_i)p_Y(Y_j)} \right)
$$
$$
= \mathcal{O}(1/N) + e^{\text{constant}} \frac{N - 1}{N} \frac{1}{N - 1} \sum_{j \neq i} \frac{p(X_i, Y_j)}{p_X(X_i)p_Y(Y_j)}
$$
$$
\to e^{\text{constant}} \mathbb{E}_{X \sim p_X, Y \sim p_Y} \left[ \frac{p(X, Y)}{p_X(X)p_Y(Y)} \right]
(\text{as } N \to \infty)$$</li>
</ul>
<p>$$\approx e^{\text{constant}} \mathbb{E}_{X \sim p_X, Y \sim p_Y} \left[ \frac{p(X, Y)}{p_X(X)p_Y(Y)} \right]
$$
$$
= e^{\text{constant}} \int_x \int_y p(x, y) dx dy
$$</p>
<ul>
<li>최종적으로, 다음과 같이 정리됩니다:</li>
</ul>
<p>$$
\mathcal{L}<em>{NCE} = \frac{1}{N} \sum</em>{i=1}^N \log \frac{e^{f_<em>(X_i, Y_i)}}{\frac{1}{N} \sum_{j=1}^N e^{f_</em>(X_i, Y_j)}}
$$
$$\approx \frac{1}{N} \sum_{i=1}^N \log \frac{p(X_i, Y_i)}{p_X(X_i)p_Y(Y_i)}
$$
$$
\approx \mathbb{E}_{(X, Y) \sim p} \left[ \log \frac{p(X, Y)}{p_X(X)p_Y(Y)} \right]
$$
$$= I(X; Y)
$$
$$
\text{Thus, the proof is complete. } \blacksquare
$$</p>
<h2 id="3-infonce-loss와-cross-entropy-loss">3. InfoNCE loss와 Cross Entropy loss</h2>
<ul>
<li><p>InfoNCE loss는 다중 클래스 classification task에서 Cross Entropy (CE) loss과 동일한 구조를 가짐.</p>
</li>
<li><p>InfoNCE loss의 각 항 $\ell_{NCE}(Y_: , X_i)$를 다음과 같이 정의
$$
\mathcal{L}<em>{NCE} = \sum</em>{i=1}^N \log \frac{e^{f(X_i, Y_i)}}{\sum_{j=1}^N e^{f(X_i, Y_j)}}
$$
$$
\ell_{NCE}(Y_: , X_i) = \log \frac{e^{f(X_i, Y_i)}}{\sum_{j=1}^N e^{f(X_i, Y_j)}}$$</p>
</li>
</ul>
<ul>
<li>각 항목 $\ell_{NCE}(Y_: , X_i)$는 $X_i$를 $N$개의 클래스로 분류하는 cross entropy 손실로 볼 수 있음.</li>
</ul>
<p>$$
P(\text{class of } X_i = j) \propto e^{f(X_i, Y_j)}
$$
$$
\ell_{CE}(F(x), i) = -\log \frac{\exp(F_i(x))}{\sum_{j=1}^k \exp(F_j(x))}
$$</p>
<ul>
<li>F: model의 pre-softmax 출력
$$
F(x; Y) = \left(f(x, Y_1), f(x, Y_2), \ldots, f(x, Y_N)\right)
$$</li>
</ul>
<ul>
<li>따라서, 결론적으로,
$$
\ell_{CE}(F(x), i) = -\log \frac{e^{F_i(x)}}{\sum_{j=1}^{k} e^{F_j(x)}}
$$ 
$$
\text{Thus, the proof is complete. } \blacksquare
$$</li>
</ul>
<h2 id="4-clip과-mutual-information-근사">4. CLIP과 Mutual Information 근사</h2>
<ul>
<li>CLIP은 MI를 근사하여 이미지와 텍스트를 동일한 잠재 공간($\mathbb{R}^d$)에 매핑.</li>
<li>데이터 처리 불평등(Data Processing Inequality)에 의해 MI의 하한을 얻음.</li>
</ul>
<h3 id="41-infonce-손실-함수">4.1 InfoNCE 손실 함수</h3>
<p>:</p>
<p>CLIP 학습은 다음 InfoNCE (Noise Contrastive Estimation) loss를 최대화:</p>
<blockquote>
<p>CLIP Loss Definition
$$
\mathcal{L}<em>{NCE}(\theta, \phi) = \frac{1}{N} \sum</em>{i=1}^N \log \frac{\exp(f_{\theta}(X_i) \cdot g_{\phi}(C_i) / \tau)}{\frac{1}{N} \sum_{j=1}^N \exp(f_{\theta}(X_i) \cdot g_{\phi}(C_j) / \tau)} + \frac{1}{N} \sum_{i=1}^N \log \frac{\exp(f_{\theta}(X_i) \cdot g_{\phi}(C_i) / \tau)}{\frac{1}{N} \sum_{j=1}^N \exp(f_{\theta}(X_j) \cdot g_{\phi}(C_i) / \tau)}
$$
Thus,
$$\mathcal{L}<em>{NCE}(\theta, \phi) \approx \sum</em>{i=1}^N \log \frac{\exp(f_{\theta}(X_i) \cdot g_{\phi}(C_i) / \tau)}{\sum_{j=1}^N \exp(f_{\theta}(X_i) \cdot g_{\phi}(C_j) / \tau)} + \sum_{i=1}^N \log \frac{\exp(f_{\theta}(X_i) \cdot g_{\phi}(C_i) / \tau)}{\sum_{j=1}^N \exp(f_{\theta}(X_j) \cdot g_{\phi}(C_i) / \tau)}
$$</p>
</blockquote>
<p>여기서:</p>
<ul>
<li><p>$f_{\theta}(X_i)$: 이미지 $X_i$의 embedding vector</p>
</li>
<li><p>$g_{\phi}(C_j)$: 텍스트 $C_j$의 embedding vector</p>
</li>
<li><p>$\tau$: 온도 매개변수(Temperature Parameter)</p>
<ul>
<li><p>$$\tau \to 0 \quad \Rightarrow$$ 분포가 sharper해지며, 가장 큰 유사도 값에 더 높은 확률을 할당.</p>
</li>
<li><p>$$\tau \to \infty \quad \Rightarrow$$ 분포가 smoother해지며, 확률이 고르게 분산.</p>
</li>
</ul>
</li>
</ul>
<ul>
<li>cf. CLIP에서 InfoNCE 손실 함수를 두 번 정의하는 이유는? <ul>
<li>텍스트-이미지 간 대칭성(symmetry)을 고려하여 양방향으로 유사성을 학습하기 위함(이미지에서 텍스트로, 텍스트에서 이미지로)</li>
</ul>
</li>
</ul>
<h3 id="42-clip과-mutual-information-근사">4.2 CLIP과 Mutual Information 근사</h3>
<p>CLIP은 Mutual Information (MI)을 근사하여 학습됩니다.</p>
<h3 id="421-mutual-information-정의">4.2.1 Mutual Information 정의</h3>
<p>Mutual Information은 다음과 같이 정의됩니다:</p>
<p>$$
I(X; C) = \int p(x, c) \log \frac{p(x, c)}{p_X(x)p_C(c)} dx dc
$$</p>
<h3 id="422-clip에서의-mi-근사">4.2.2 CLIP에서의 MI 근사</h3>
<ul>
<li>CLIP은 임베딩 벡터 $f_{\theta}(X)$와 $g_{\phi}(C)$를 학습하여, 두 벡터의 내적 $f_{\theta}(X) \cdot g_{\phi}(C)$가:<ul>
<li>$X$와 $C$가 연관될 때 최대화.</li>
<li>연관되지 않을 때 최소화되도록 합니다.</li>
</ul>
</li>
</ul>
<p>데이터 처리 부등식(Data Processing Inequality)에 따르면:</p>
<p>$$
I(X; C) \geq I(f_{\theta}(X); C) \geq I(f_{\theta}(X); g_{\phi}(C))
$$</p>
<p>이 부등식은 CLIP 모델이 Mutual Information의 하한을 학습한다는 것을 보여줍니다.</p>
<h3 id="43-infonce와-mi의-관계">4.3 InfoNCE와 MI의 관계</h3>
<p>이전 분석에 따르면 다음이 성립합니다:</p>
<p>$$
I(X; C) \geq \mathbb{E}[\mathcal{L}<em>{NCE}]=I(f</em>{\theta}(X); g_{\phi}(C)) \geq \frac{1}{2} \mathcal{L}_{NCE}
$$</p>
<ul>
<li>$N \to \infty$일 때, $I(X; C) = \frac{1}{2} \mathcal{L}_{NCE}$의 상한에 도달</li>
</ul>
<p>또한, 최적의 임베딩 함수 $f_{\theta}^<em>(X)$와 $g_{\phi}^</em>(C)$는 다음과 같이 표현됩니다:</p>
<p>$$
f_{\theta}^<em>(X) \cdot g_{\phi}^</em>(C) + \text{constant} = \tau \log \frac{p(X, C)}{p(X)p(C)} = \tau \log p(C | X) - \tau \log p(C)
$$</p>
<ul>
<li>(이는 Mutual Information의 직접적인 근사로 볼 수 있음)</li>
</ul>
<h2 id="5-clip의-이론적-기반-joint-embedding의-보편성-universality-of-joint-embeddings">5. CLIP의 이론적 기반: Joint Embedding의 보편성 (Universality of Joint Embeddings)</h2>
<ul>
<li>임의의 함수 $h(X, C)$를 근사하는 embedding $f_\theta(X), g_\phi(C)$를 찾을 수 있는가?<ul>
<li>$d \to \infty$일 때 보편 근사 (Universal Approximation) 가능.</li>
</ul>
</li>
</ul>
<h3 id="51-universality-of-joint-embeddings의-정의-및-배경">5.1 Universality of Joint Embeddings의 정의 및 배경</h3>
<ol>
<li><p>$\mathcal{X}$와 $\mathcal{Y}$는 국소 콤팩트 하우스도르프(LCH, Locally Compact Hausdorff) 공간이다.</p>
<ul>
<li>$\mathcal{X}$: 이미지 공간 (보통 $\mathbb{R}^n$으로 표현).</li>
<li>$\mathcal{Y}$: 문장 공간 (이산 공간 $\mathcal{V}^*$로 표현).</li>
</ul>
</li>
<li><p>$\mathcal{F} \subset C(\mathcal{X}; \mathbb{R})$, $\mathcal{G} \subset C(\mathcal{Y}; \mathbb{R})$는 각각 $\mathcal{X}$와 $\mathcal{Y}$에서 정의된 연속 함수의 벡터 공간에서 조밀한 부분 공간(dense sub-vector space)이다.</p>
</li>
</ol>
<hr />
<h3 id="52-stone-weierstrass-정리">5.2 Stone-Weierstrass 정리</h3>
<p>Stone-Weierstrass 정리에 따르면, 다음 집합은 $\mathcal{C}(\mathcal{X} \times \mathcal{Y}; \mathbb{R})$에서 균등 수렴 위상(uniform convergence topology) 하에 조밀하다:
$$
\left{ \sum_{k=1}^d f_k(x)g_k(y) \ \middle| \ f_k \in \mathcal{F}, g_k \in \mathcal{G}, d \in \mathbb{N} \right} \subset C(\mathcal{X} \times \mathcal{Y}; \mathbb{R}).
$$</p>
<p>따라서, $\mathcal{X} \times \mathcal{Y}$에서 정의된 임의의 연속 함수 $h(x, y)$는 충분히 큰 $d$에 대해:
$$
h(x, y) \approx \sum_{k=1}^d f_k(x)g_k(y),
$$
형태로 근사 가능.</p>
<hr />
<h3 id="53-hilbert-공간에서의-보편성">5.3 Hilbert 공간에서의 보편성</h3>
<p>Hilbert 공간 $L^2(\mathcal{X}; \mathbb{R})$와 $L^2(\mathcal{Y}; \mathbb{R})$가 분리 가능(separable)할 때:
$$
L^2(\mathcal{X}; \mathbb{R}) \otimes L^2(\mathcal{Y}; \mathbb{R}) = L^2(\mathcal{X} \times \mathcal{Y}; \mathbb{R}),
$$
다음 집합은 조밀하다:
$$
\left{ \sum_{k=1}^d f_k(x)g_k(y) \ \middle| \ f_k \in L^2(\mathcal{X}; \mathbb{R}), g_k \in L^2(\mathcal{Y}; \mathbb{R}), d \in \mathbb{N} \right} \subset L^2(\mathcal{X} \times \mathcal{Y}; \mathbb{R}).
$$</p>
<blockquote>
<p>즉, $h_{\theta, \phi}(x, y) = f_{\theta}(x) \cdot g_{\phi}(y)$는 $d \to \infty$일 때 보편 근사기로 작동한다.</p>
</blockquote>
<hr />
<h3 id="54-joint-embedding의-보편성">5.4 Joint Embedding의 보편성</h3>
<blockquote>
<ul>
<li>주어진 $f_{\theta}$와 $g_{\phi}$가 보편 근사기(universal approximators)일 때, 다음이 성립한다:
$$
h_{\theta, \phi}(x, y) = f_{\theta}(x) \cdot g_{\phi}(y) = \sum_{k=1}^d (f_{\theta}(x))<em>k \cdot (g</em>{\phi}(y))_k.
$$</li>
<li>충분히 큰 $d$에 대해, $h_{\theta, \phi}(x, y)$는 임의의 함수 $h(x, y)$를 근사할 수 있다.</li>
</ul>
</blockquote>
<hr />
<h3 id="55-결론">5.5 결론</h3>
<ul>
<li>$\mathcal{X}$와 $\mathcal{Y}$의 joint embedding을 통해 정의된 $f_{\theta}(x) \cdot g_{\phi}(y)$는 보편 근사 성질을 가지며, 이를 통해 임의의 복합적 함수 $h(x, y)$를 표현할 수 있다.</li>
<li>$d \to \infty$와 $f_{\theta}(x), g_{\phi}(y)$의 깊이(depth)가 충분할 경우 이 보편 근사 성질이 성립한다.</li>
</ul>
<h2 id="6-결론">6. 결론</h2>
<ul>
<li>CLIP과 같은 Vision-Language 모델은 Mutual Information을 근사하도록 학습됨.</li>
<li>InfoNCE 손실은 Mutual Information의 하한을 제공하며, $N \to \infty$일 때 정확한 근사 가능.</li>
<li>Joint Embedding 구조가 보편 근사 능력을 가지기 때문에 가능한 모델.</li>
</ul>
<hr />
<hr />
<hr />
<h2 id="필자의-궁금증">필자의 궁금증</h2>
<h3 id="f-cdot-g--tau로-유사도를-정의하고-그걸로-mathcall_nce를-정의한-뒤-극한을-보내면-mi가-되는가">$f \cdot g / \tau$로 유사도를 정의하고, 그걸로 $\mathcal{L}_{NCE}$를 정의한 뒤 극한을 보내면 MI가 되는가?**</h3>
<ul>
<li><p><strong>InfoNCE 손실 함수</strong>:
InfoNCE는 $f \cdot g / \tau$를 사용해 데이터 간 유사도를 측정하고, 이를 바탕으로 정답 쌍과 오답 쌍 간의 구별 능력을 학습함.
$$
\mathcal{L}<em>{NCE} = - \frac{1}{N} \sum</em>{i=1}^N \log \frac{\exp(f_{\theta}(X_i) \cdot g_{\phi}(C_i) / \tau)}{\sum_{j=1}^N \exp(f_{\theta}(X_i) \cdot g_{\phi}(C_j) / \tau)}.
$$</p>
</li>
<li><p><strong>Mutual Information으로의 수렴</strong>:</p>
<ul>
<li><p>InfoNCE 손실은 다음 조건에서 Mutual Information에 수렴함:</p>
<ol>
<li>$N \to \infty$일 때:
$$
\lim_{N \to \infty} \mathcal{L}_{NCE} = I(X; C).
$$</li>
<li>최적의 임베딩 함수 $f_{\theta}^<em>(X)$와 $g_{\phi}^</em>(C)$를 사용:
$$
f_{\theta}^<em>(X) \cdot g_{\phi}^</em>(C) = \tau \log \frac{p(X, C)}{p(X)p(C)} + \text{constant}.
$$</li>
</ol>
</li>
<li><p>극한에서 InfoNCE는 다음과 같이 MI로 변환됨:
$$
\mathcal{L}_{NCE} \to \mathbb{E} \left[ \log \frac{p(X, C)}{p(X)p(C)} \right] = I(X; C).
$$</p>
</li>
</ul>
</li>
</ul>
<hr />
<ul>
<li><strong>결론</strong>:
$p(x, y)$는 $X$와 $Y$ 간의 결합 확률을 나타내며, 이를 CLIP에서는 내적 $f_{\theta}(X) \cdot g_{\phi}(C)$로 정의한 것임:<ul>
<li>왜 이러한 모델링이  가능한가? 자세한 증명: #5의 Universality of Joint Embeddings 파트와 관련이 있음.</li>
</ul>
</li>
</ul>
<ol>
<li><strong>모델링 선택</strong>:<ul>
<li>$f_{\theta}(X) \cdot g_{\phi}(C)$가 $p(X, C)$를 근사한다고 가정하지만, 이를 증명하려면:
$$
f_{\theta}(X), g_{\phi}(C), p(X, C)
$$
의 함수 공간, 학습 과정, 데이터 분포 등을 포함한 엄밀한 분석이 필요함.</li>
<li>이 가정은 경험적 근사에 기반을 둠. + Universality of Joint Embeddings 이론 기반 설명</li>
</ul>
</li>
</ol>