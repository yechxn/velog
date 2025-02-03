<h1 id="lecture-2-cellular-communication-ap-propagation--nervous-system">Lecture 2, Cellular Communication: AP Propagation &amp; Nervous System</h1>
<ul>
<li>Ref: Pf. Kang's SNUCM Lectures</li>
</ul>
<h2 id="1-nervous-system">1. Nervous System</h2>
<p><img alt="" src="https://velog.velcdn.com/images/yechxn/post/fb8367c2-b1d9-446e-847f-cd6b6d5fe0d4/image.png" />
<img alt="" src="https://velog.velcdn.com/images/yechxn/post/d9cb4eb4-5ec4-47e9-85fe-d8555e1d7e0e/image.png" /></p>
<h2 id="2-cable-equation--action-potential-propagation">2. Cable Equation : Action Potential Propagation</h2>
<p><img alt="" src="https://velog.velcdn.com/images/yechxn/post/6dc71927-7e87-404d-af1e-ffe83491e539/image.png" /></p>
<ul>
<li>KCL, KVL: Kirchhoff's Current / Voltage Law
<img alt="" src="https://velog.velcdn.com/images/yechxn/post/b031dbfb-dc6d-4308-bde9-311e67f071d9/image.png" /></li>
</ul>
<blockquote>
<p><strong>가정</strong></p>
</blockquote>
<ol>
<li>1D model</li>
<li>Inside: 단위길이당 저항 : $$R_c$$</li>
<li>Outside: 저항 : $$0$$</li>
<li>세포막 단위길이 당 Capacitance : $$C_m$$</li>
<li>세포막 단위길이 당 Cunductance : $$\frac{1}{R_m}$$ (ions leaky chn.)</li>
</ol>
<h3 id="2-1-kcl">2-1. KCL</h3>
<p><img alt="" src="https://velog.velcdn.com/images/yechxn/post/3d35e8a0-ad48-4a4e-a89a-f6f72bcbaa09/image.png" /></p>
<ul>
<li><p>dx: 1D 세포막 길이</p>
<ul>
<li>축전용량: dx에 비례 (bc. 세포막 넓이에 비례) </li>
<li>저항: dx에 반비례 (bc. 세포막 넓이에 반비례)
$$
C = C_m , dx, \quad R = \frac{R_m}{dx}
$$</li>
</ul>
</li>
<li><p>KCL at #1
$$
i + i_c + i_{R_m} = i + di 
$$
Thus, 
$$
di = i_c + i_{R_m}
$$</p>
<ul>
<li><p>축전기
$$
Q = C , V = C_m , dx , V
$$
$$
i_c = \frac{dQ}{dt} = \frac{d}{dt} \left( C_m , dx , V \right) = C_m , dx , \frac{dV}{dt}
$$</p>
</li>
<li><p>저항
$$
i_{R_m} = \frac{V}{R_m} , dx
$$</p>
</li>
<li><p>=&gt; KCL 대입
$$
di = C_m , dx , \frac{dV}{dt} + \frac{V}{R_m} , dx
$$</p>
</li>
</ul>
</li>
</ul>
<blockquote>
<p>최종 식 (1)
$$
R_m \frac{d i}{dx} = R_m , C_m , \frac{dV}{dt} + V
$$</p>
</blockquote>
<h3 id="2-2-dv-eq">2-2. dV eq.</h3>
<p><img alt="" src="https://velog.velcdn.com/images/yechxn/post/a93f65b0-6bf5-46c7-8481-10f2a727800b/image.png" /></p>
<ul>
<li><p>dV
$$dV = i , R_c , dx
$$
Thus,
$$i = \frac{1}{R_c} \frac{dV}{dx} 
$$</p>
</li>
<li><p>최종 식 (1)에 대입</p>
<blockquote>
<p>최종 식 (2)
$$
R_m \frac{1}{R_c} \frac{d^2 V}{dx^2} = R_m C_m \frac{dV}{dt} + V
$$</p>
</blockquote>
</li>
<li><p>상수 정의</p>
<ul>
<li>길이 상수 (cable space constant) ~ 150um
$$\lambda_m^2 = \frac{R_m}{R_c}
$$
즉, 
$$\lambda_m = \sqrt{\frac{R_m}{R_c}}
$$</li>
<li>시간 상수 (membrane time constant) ~ 8.4ms
$$\tau_m = R_m C_m
$$</li>
</ul>
</li>
</ul>
<h3 id="2-3-cable-equation">2-3. Cable equation</h3>
<p><img alt="" src="https://velog.velcdn.com/images/yechxn/post/3e32446c-e50c-44e4-9a95-201b3c9d6305/image.png" /></p>
<blockquote>
<p><strong>Cable equation</strong>
$$
\lambda_m^2 \frac{\partial^2 V}{\partial x^2} = \tau_m \frac{\partial V}{\partial t} + V
$$</p>
</blockquote>
<h3 id="2-4-ap-propagation">2-4. AP Propagation</h3>
<p><img alt="" src="https://velog.velcdn.com/images/yechxn/post/036a8516-a4d3-463e-ba89-892f59a11989/image.png" /></p>
<ul>
<li><p>Steady State: $$dV/dt = 0$$
$$\lambda_m^2 \frac{d^2 V}{dx^2} = V
$$
즉,</p>
<blockquote>
<p><strong>Steady State:</strong>
$$V(x) = V_0 e^{-\frac{x}{\lambda_m}}
$$</p>
</blockquote>
</li>
<li><p>가정</p>
<ul>
<li>$$V_0 = 100mV$$</li>
<li>AP threshold $$= -60 + 20 (mV)$$</li>
<li>$$\lambda_m=150\mu m$$</li>
</ul>
</li>
<li><p>Maximum distance (AP peak-to-peak)</p>
<ul>
<li>계산 방법
$$V(x) \geq 20
$$
즉,
$$100 e^{-\frac{x}{150}} \geq 20
$$
$$x \leq 150 \ln{5} = 240(\mu m) 
$$</li>
<li>Maximum AP p2p distance는$$\lambda_m$$에 비례</li>
</ul>
</li>
<li><p>Nerve의 diameter가 커질수록, $$R_c$$ 감소 -&gt; $$\lambda_m$$ 증가 -&gt; AP propagation 속도 증가(p2p 거리 증가)</p>
</li>
</ul>
<blockquote>
<p><strong>AP 전파 속도</strong></p>
</blockquote>
<ol>
<li>$$\lambda_m$$에 비례</li>
<li>Nerve Diameter에 비례</li>
</ol>
<h3 id="2-5-ranvier-nodes">2-5. Ranvier nodes</h3>
<p><img alt="" src="https://velog.velcdn.com/images/yechxn/post/6753aa4a-3ccf-40ba-9aa2-a0b6d49aac5a/image.png" />
<img alt="" src="https://velog.velcdn.com/images/yechxn/post/4f498f1d-1f06-43e2-84be-4932ce970ae2/image.png" /></p>
<ul>
<li>Larger $$R_m$$</li>
</ul>
<h2 id="2-cellular-communication">2. Cellular Communication</h2>
<h3 id="2-1-synapses">2-1. Synapses</h3>
<ul>
<li><p>Chemical Synapse
<img alt="" src="https://velog.velcdn.com/images/yechxn/post/4c44cebf-b3f3-4fb3-9787-f9faa7d56131/image.png" /></p>
</li>
<li><p>Electrical Synapse </p>
<ul>
<li>ex. Cardiac muscle cells
<img alt="" src="https://velog.velcdn.com/images/yechxn/post/cb93cd71-8700-407b-bdb3-107dcabcf12d/image.png" /></li>
</ul>
</li>
</ul>
<h3 id="2-2-neuromuscular-junction">2-2. Neuromuscular junction</h3>
<ul>
<li>Neuromuscular junc.<ul>
<li>{1 motor neuron} for {1 muscle cell} synapse</li>
<li>$$\sum$$EPSP = AP (in post synaptic neuron)<ul>
<li>Temporal Summation</li>
<li>Spatial Summation
<img alt="" src="https://velog.velcdn.com/images/yechxn/post/bddabdc8-f5bd-4780-bfca-69fa9694cba7/image.png" /></li>
</ul>
</li>
</ul>
</li>
</ul>
<p><img alt="" src="https://velog.velcdn.com/images/yechxn/post/b1480cf8-2b50-4c5a-bb9a-72239e0c3e7a/image.png" /></p>
<h3 id="2-3-epsp--ipsp">2-3. EPSP &amp; IPSP</h3>
<ul>
<li>Excitatory postsynaptic potential (EPSP)<ul>
<li>Post synaptic cell: Depol</li>
</ul>
</li>
<li>Inhibitory postsynaptic potential (IPSP)<ul>
<li>Post synaptic cell: Hyperpol
<img alt="" src="https://velog.velcdn.com/images/yechxn/post/29a27e2b-1d1b-48dc-9e48-c34d900e8359/image.png" /></li>
</ul>
</li>
</ul>
<h2 id="3-cardiac-muscle-cells-heart">3. Cardiac Muscle cells: Heart</h2>
<h3 id="3-1-ap-in-cardiac-muscle-cells">3-1. AP in Cardiac Muscle Cells</h3>
<p><img alt="" src="https://velog.velcdn.com/images/yechxn/post/84789809-2633-4491-bce3-121cca059909/image.png" /></p>
<ul>
<li>Ca2+ 차이</li>
</ul>
<p><img alt="" src="https://velog.velcdn.com/images/yechxn/post/38c57b31-df5a-4829-ad36-0d3d0582cae2/image.png" /></p>
<h3 id="3-2-ap-in-san-sa-node-cells">3-2. AP in SAN (SA Node) Cells</h3>
<p><img alt="" src="https://velog.velcdn.com/images/yechxn/post/4166e636-ba33-4298-8873-31c7589b4860/image.png" /></p>
<blockquote>
<p>Nervous system ~ electrical circuit (bioelectronics system)</p>
</blockquote>