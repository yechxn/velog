<h1 id="생체계측공학-lecture-3-electrochemical-principles--electrode-reactions">[생체계측공학] Lecture 3, Electrochemical Principles &amp; Electrode Reactions</h1>
<h2 id="1-개요-overview"><strong>1. 개요 (Overview)</strong></h2>
<p>본 문서는 생체계측공학(Bioinstrumentation)에서 중요한 전기화학적 원리와 전극 반응(Electrode Reactions)에 대해 다룹니다. 주요 내용은 다음과 같습니다:</p>
<ul>
<li><strong>전극-전해질 계면의 등가 회로 모델링</strong><ol>
<li><strong>전기 이중층(Electrical Double Layer, EDL) 모델</strong></li>
<li><strong>전기화학적 반응(산화/환원, Oxidation/Reduction)과 임피던스 특성 분석</strong></li>
<li><strong>전기화학적 임피던스 분광법(EIS, Electrochemical Impedance Spectroscopy)</strong></li>
</ol>
</li>
</ul>
<hr />
<h2 id="2-design-rule--impedance-matching"><strong>2. Design Rule = Impedance Matching</strong></h2>
<ul>
<li>이상적으로, $V_{in} = V_{Read}$이길 바람<ul>
<li>하지만, Interface에 의한 $R$이 생길 수밖에 없고, 이로 인해 interface를 회로로 모델링하는 것이 중요하다.</li>
<li>Input 임피던스를 무한대로 보내어, $R$에 의한 전압 loss를 최소화하고, Voltage Divider에서 Recorder에 걸리는 전압을 최대로 해야 한다.</li>
<li>반대로, 자극하는 경우 중간단계의 저항을 최소화하여 Energy loss를 줄여야 한다.</li>
</ul>
</li>
</ul>
<hr />
<h2 id="part-1-inert-metal-가정--edl-모델링"><strong>Part 1: Inert Metal 가정 – EDL 모델링</strong></h2>
<h3 id="1-전기-이중층-edl-모델"><strong>(1) 전기 이중층 (EDL) 모델</strong></h3>
<p><img alt="" src="https://velog.velcdn.com/images/yechxn/post/0fdee921-316e-4f0d-affc-d4f95d5e9e71/image.png" /></p>
<ul>
<li>전극-전해질 계면에서 형성되는 <strong>전기 이중층(Electrical Double Layer, EDL)</strong></li>
<li>축전용량 모델 논의:<ul>
<li>이온의 직경까지만 고려하여 $d$를 결정할 것인가?</li>
<li>Debye 길이까지 포함하여 고려할 것인가?</li>
<li>단순 평판 축전기가 아닌 <strong>Double Layer 모델</strong> 적용 필요</li>
</ul>
</li>
</ul>
<h3 id="2-helmholtz-및-gouy-chapman-stern-모델"><strong>(2) Helmholtz 및 Gouy-Chapman-Stern 모델</strong></h3>
<ul>
<li><strong>(a) Helmholtz 모델:</strong> 평행판 축전기로 단순 모델링</li>
<li><strong>(b) Gouy-Chapman 모델:</strong> 확산층 고려</li>
<li><strong>(c) Gouy-Chapman-Stern (GCS) 모델:</strong> 두 가지 모델을 결합하여 보다 현실적인 모델 구성</li>
</ul>
<p><img alt="" src="https://velog.velcdn.com/images/yechxn/post/3ef46ed6-8aed-453c-ad82-8e7c750a58eb/image.png" /></p>
<h3 id="3-debye-길이-debye-length"><strong>(3) Debye 길이 (Debye Length)</strong></h3>
<p>Debye 길이는 전해질 내에서 전기적인 차폐 효과를 설명하는 길이 척도입니다.</p>
<p>$$
\lambda_D = \frac{1}{\kappa} = \sqrt{\frac{\varepsilon_0 \varepsilon_r kT}{q^2 \sum_i z_i^2 c_{i\infty}}}
$$</p>
<ul>
<li>$\kappa$: 역 Debye 길이</li>
<li>$\varepsilon_0$: 진공 유전율</li>
<li>$\varepsilon_r$: 상대 유전율</li>
<li>$T$: 절대 온도</li>
<li>$q$: 기본 전하량</li>
<li>$z_i$: 이온의 원자가수</li>
<li>$c_{i\infty}$: 벌크 용액 내 이온 농도</li>
</ul>
<h3 id="4-면적당-정전용량-areal-capacitance"><strong>(4) 면적당 정전용량 (Areal Capacitance)</strong></h3>
<p>면적당 정전용량은 다음과 같이 정의됩니다:</p>
<p>$$
\frac{C}{A} = \left( \varepsilon_0 \varepsilon_r \frac{1}{\kappa} \right) = \left( \frac{\varepsilon_0 \varepsilon_r}{\text{Debye length}} \right)
$$</p>
<p>총 정전용량은 다음과 같이 표현할 수 있습니다:</p>
<p>$$
C = \frac{dQ}{dV} = \frac{dQ}{dA}
$$</p>
<hr />
<h2 id="part-2-산화환원-고려--병렬-연결-저항--이온순환-z_w"><strong>Part 2: 산화/환원 고려 – 병렬 연결 저항 + 이온순환 $Z_w$</strong></h2>
<p><img alt="" src="https://velog.velcdn.com/images/yechxn/post/161844a6-80a4-473d-b954-9369ae43fe1f/image.png" /></p>
<h3 id="1-왜-병렬-연결-모델을-사용하는가"><strong>(1) 왜 병렬 연결 모델을 사용하는가?</strong></h3>
<ul>
<li>산화/환원 반응이 적어지면 $R_{ct}$가 증가<ul>
<li>그에 따라 <strong>전류의 대부분이 $C_{dl}$을 통해 흐르게 됨</strong></li>
</ul>
</li>
<li>따라서, 병렬 연결 모델이 적절</li>
</ul>
<h3 id="2-warburg-임피던스-z_w와-이온-순환"><strong>(2) Warburg 임피던스 $Z_w$와 이온 순환</strong></h3>
<p><img alt="" src="https://velog.velcdn.com/images/yechxn/post/efbc9f2a-e5a7-459a-9624-6e3ea444b1f3/image.png" /></p>
<ul>
<li>Warburg 임피던스는 <strong>이온 순환을 모델링</strong>한 개념<ul>
<li>산화/환원 반응만 모델링한 $R_{ct}$에 더하여, 이온 순환(mass transfer)까지 고려한 모델<ul>
<li>ex1) 저주파 영역에서는 이온 순환 증가 → $Z_W$ 감소 → 더 많은 전류 흐름</li>
<li>ex2) 접촉이 불량하면 이온 순환 감소 → $Z_W$ 증가 → 저주파에서도 전류 흐름 제한</li>
</ul>
</li>
</ul>
</li>
</ul>
<hr />
<h2 id="part-3-characterization--eis-bode-plot-nyquist-plot"><strong>Part 3: Characterization – EIS, Bode Plot, Nyquist Plot</strong></h2>
<p><img alt="" src="https://velog.velcdn.com/images/yechxn/post/aee5fe67-7773-4cb5-bbe6-77f307a3c274/image.png" /></p>
<h3 id="1-lcr-meter를-통한-데이터-측정"><strong>(1) LCR meter를 통한 데이터 측정</strong></h3>
<ul>
<li>EIS (Electrochemical Impendence Spectroscopy)에서 임피던스는 다음과 같이 측정됨:</li>
</ul>
<p>$$
Z = \frac{V(t)}{I(t)}
$$</p>
<ul>
<li>주파수별 전압과 전류를 측정하여 임피던스 스펙트럼을 얻음</li>
</ul>
<h3 id="2-bode-plot과-nyquist-plot"><strong>(2) Bode Plot과 Nyquist Plot</strong></h3>
<ul>
<li><p><strong>Bode Plot:</strong>
<img alt="" src="https://velog.velcdn.com/images/yechxn/post/02c3d659-23e4-4afa-8890-cf4f97df6f15/image.png" /></p>
<p>$$
|Z| = \sqrt{R_{ct}^2 + \left(\frac{1}{\omega C}\right)^2}
$$</p>
<p>$$
\phi = \tan^{-1}\left(\frac{-1}{\omega R_{ct} C}\right)
$$</p>
</li>
<li><p><strong>Nyquist Plot:</strong></p>
</li>
</ul>
<p><img alt="" src="https://velog.velcdn.com/images/yechxn/post/ad84c8a0-24c6-445b-98d6-cf272b8d5e08/image.png" />
<img alt="" src="https://velog.velcdn.com/images/yechxn/post/bc351539-82f3-4484-b9b6-9ba1e180d45c/image.png" /></p>
<p>  $$
  \left(Re(Z) - \frac{R_{ct}}{2}\right)^2 + \left(Im(Z)\right)^2 = \left(\frac{R_{ct}}{2}\right)^2
  $$</p>
<ul>
<li>$Z_W$를 고려하면 <strong>고주파에서는 원을 따르고, 저주파에서는 직선형태로 수렴</strong></li>
</ul>
<hr />
<h2 id="4-reference-electrode의-역할"><strong>4. Reference Electrode의 역할</strong></h2>
<h3 id="1-reference-electrode-크기의-중요성"><strong>(1) Reference Electrode 크기의 중요성</strong></h3>
<ul>
<li>Reference electrode의 면적 $A$가 커지면:<ul>
<li>정전용량 $C$이 증가 → $Z = \frac{1}{j\omega C}$가 작아짐</li>
<li>저항 $R$도 감소 
→ 회로에서 인터페이스 효과를 무시 가능</li>
</ul>
</li>
</ul>
<h3 id="2-agagcl-reference-electrode의-특성"><strong>(2) Ag/AgCl Reference Electrode의 특성</strong></h3>
<ul>
<li><strong>산화/환원 반응이 매우 활발</strong> → <strong>전하 이동 저항 ($R_{ct}$ )이 거의 0에 가까움</strong><ul>
<li>인터페이스에서 발생하는 전기화학적 반응이 미미하여 <strong>회로 성능에 영향을 주지 않음</strong></li>
</ul>
</li>
<li>이러한 특성 덕분에 <strong>ECG, EEG, 초음파 젤 등과 같은 생체 신호 측정에 널리 사용됨</strong></li>
</ul>
<hr />
<h2 id="5-참고-문헌"><strong>5. 참고 문헌</strong></h2>
<ul>
<li>Pethig, <em>Electrochemical Principles and Electrode Reactions</em>, Chapter 3, 4, 5</li>
<li>DOI: <a href="https://doi.org/10.33961/jecst.2019.00528">10.33961/jecst.2019.00528</a></li>
</ul>