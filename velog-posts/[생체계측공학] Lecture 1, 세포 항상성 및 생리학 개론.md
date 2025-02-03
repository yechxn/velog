<h1 id="lecture-1-cellular-homeostasis--biophysical-concepts">Lecture 1, Cellular Homeostasis &amp; Biophysical Concepts</h1>
<ul>
<li>Ref: Pf. Kang's SNUCM Lectures</li>
<li>의대생이시면, 본1 전기생리학 강의 참고</li>
</ul>
<h2 id="1-ph가-protein의-전기적-성질을-결정">1. pH가 protein의 전기적 성질을 결정</h2>
<ul>
<li>H+와 OH-의 균형에 따라 protein의 다음 작용기 성질이 변화<ul>
<li>Carboxyl side group : -COOH</li>
<li>Amino side group : -NH2
=&gt; 이에 따라, protein의 다음 성질들이 변화함</li>
</ul>
</li>
</ul>
<ol>
<li>Electrophoretic mobility</li>
<li>Electrostatic interactions</li>
<li>Enzyme activity (E+S binding: Electrostatic interactions)</li>
</ol>
<blockquote>
<p>따라서, pH value는 효소 활성도 (Enzyme activity)를 결정
=&gt; 생체계측에서는 pH monitoring이 매우 중요</p>
</blockquote>
<h2 id="2-ph-sensors-devices">2. pH sensors: devices</h2>
<ul>
<li>다양한 디바이스가 존재</li>
<li>ex. <a href="https://ieeexplore.ieee.org/document/7161419">https://ieeexplore.ieee.org/document/7161419</a></li>
</ul>
<h2 id="3-side-chains-hydrophillic--hydrophobic">3. Side Chains: Hydrophillic &amp; Hydrophobic</h2>
<ul>
<li>Basic rules<ol>
<li>Hydrophobic: C + nonpolar group (수소결합 가능 X)<ul>
<li>ex. Hydrocarbon chain</li>
</ul>
</li>
<li>Hydrophilic: 
(1) O, N (수소결합 가능 O)
(2) Ionisable groups 
(3) Polar groups<ul>
<li>ex. Carboxyl group (COO-, NH3+, NH2+)</li>
</ul>
</li>
</ol>
</li>
</ul>
<h2 id="4-nernset-equation-equilibrium-potential-calculation">4. Nernset equation: Equilibrium potential calculation</h2>
<p>$$
E_X = V_\text{in} - V_\text{out} = \frac{RT}{ZF} \ln \left( \frac{[X]_\text{out}}{[X]_\text{in}} \right)
$$</p>
<ul>
<li>Nernst potential: Themodynamic equilibrium (osmotic(diffusion) = electrical(drift))<ul>
<li>Permeable ions 에 대한 계산식</li>
<li>Semi-permeable or impermeable -&gt;  삼투균형 / 전기 중성 사용</li>
</ul>
</li>
</ul>
<h2 id="5-gibbs-donnan-equillibrium-equation">5. Gibbs-Donnan equillibrium equation</h2>
<ul>
<li>Gibbs-Donnan Equillibrium eq.
$$ \left[ K^+ \right]_\text{in} \left[ Cl^- \right]_\text{in} = \left[ K^+ \right]_\text{out} \left[ Cl^- \right]_\text{out}
$$</li>
</ul>
<blockquote>
<ul>
<li>세포 항상성의 조건 세가지</li>
</ul>
</blockquote>
<ol>
<li>삼투 균형 (내부/외부)</li>
<li>전기적 중성 (각 구역)</li>
<li>깁스-도난 평형식 (permeable ions)</li>
</ol>
<p>=&gt; 실제로 Na+는 자유롭게 움직이는 채널 존재 (leak chn.)
=&gt; Na+-K+ pump를 통해 지속적으로 Na+ outside로 pumping out = steady state
(mitochondria에서 생성되는 ATP의 1/3이 이 펌프에 쓰임)</p>
<h2 id="6-goldman-goldmanhodgkinkatz-equation">6. Goldman (Goldman–Hodgkin–Katz) equation</h2>
<p>$$E_m = 58 , \text{mV} \cdot \log_{10} \left( \frac{\left[ K^+ \right]_o + b \left[ Na^+ \right]_o}{\left[ K^+ \right]_i + b \left[ Na^+ \right]_i} \right)
$$</p>
<ul>
<li>p is permeability</li>
<li>K+ (high permeability): largest effect.</li>
<li>Changes in permeability (both K+, Na+) will produce large change in Em.</li>
</ul>
<p>$$
\begin{aligned}
&amp;\bullet ; b = \frac{p_\text{Na}}{p_\text{K}} \approx 0.02 \
&amp;\bullet ; E_m = -70.9 , \text{mV} \
\end{aligned}
$$</p>
<p>$$
\begin{array}{|c|c|c|}
\hline
\textbf{Ion} &amp; \textbf{Internal Concentration (mM)} &amp; \textbf{External Concentration (mM)} \
\hline
K^+ &amp; 125 &amp; 5 \
\hline
Na^+ &amp; 12 &amp; 120 \
\hline
Cl^- &amp; 5 &amp; 125 \
\hline
P^* &amp; 108 &amp; 0 \
\hline
H_2O &amp; 55,000 &amp; 55,000 \
\hline
\end{array}</p>
<p>$$</p>
<ul>
<li>in/out 이온 농도가 왜 이렇게 결정되어있는지는 원시세계 환경과 관련 있다는 설이 많음...</li>
</ul>
<h2 id="7-equivalent-circuit-for-cell-membrane">7. Equivalent Circuit for Cell Membrane</h2>
<p><img alt="" src="https://velog.velcdn.com/images/yechxn/post/5e95d9a6-85a2-4bc8-bca5-04fed7668908/image.png" /></p>
<ul>
<li>Nernst potential model -&gt; DC battery</li>
<li>Cell membrane -&gt; Capacitor (C_m)
<img alt="" src="https://velog.velcdn.com/images/yechxn/post/1b5465f6-5ea9-4f93-b79d-15d507597229/image.png" /></li>
</ul>
<h2 id="8-action-potential">8. Action Potential</h2>
<ul>
<li>GHK eq. : Na+ permeability (~b=p_Na/p_K) 가 증가 시 Em 증가<ul>
<li>보통, Na+ chn. open 시 b=0.02 -&gt; b=20 으로 증가</li>
<li>E_m의 평소값 = -81mV -&gt; E_Na=58mV 를 상한으로 증가 (log 함수꼴)<ul>
<li>E_m 변화 시 Drift &gt; Diffusion =&gt; Steady State는 깨지고, ions current 발생 </li>
</ul>
</li>
</ul>
</li>
<li>Depol = Na+: p_m 증가 -&gt; b 증가</li>
<li>Repol = Na+: h에 의해 block / K+: p_n 증가 -&gt; b 감소</li>
<li>Hyperpol: undershoot</li>
<li>Refactory period: h gate closed</li>
<li>이 과정: ms 단위 속도 =&gt; 1kHz 이상 freq로 sensing해야 함</li>
</ul>
<h2 id="9-bioelectronics-applications-using-the-h-h-hodgkin-huxley-model-models">9. Bioelectronics applications using the H-H (Hodgkin-Huxley Model) models</h2>
<ul>
<li>Hodgkin-Huxley Model</li>
</ul>
<p>$$C_m \frac{dv}{dt} = -\bar{g}<em>K n^4 (v - v_K) - \bar{g}</em>{\text{Na}} m^3 h (v - v_{\text{Na}}) - \bar{g}<em>L (v - v_L) + I</em>{\text{app}}
$$</p>
<p>$$\text{where} \quad g_K = \bar{g}<em>K n^4 \quad \text{and} \quad g</em>{\text{Na}} = \bar{g}_{\text{Na}} m^3 h
$$</p>
<ul>
<li>Simulation: <a href="http://www.cs.cmu.edu/~dst/HHsim/">http://www.cs.cmu.edu/~dst/HHsim/</a></li>
</ul>
<p><img alt="" src="https://velog.velcdn.com/images/yechxn/post/9d367c84-344e-470e-b295-0e9254bfbcc3/image.png" />
<img alt="" src="https://velog.velcdn.com/images/yechxn/post/2b2bb8b7-b2d6-4550-9c28-1d1dea011192/image.png" /></p>