<h1 id="slicerros2-a-research-and-development-module-for-image-guided-robotic-interventions"><strong>SlicerROS2: A Research and Development Module for Image-Guided Robotic Interventions</strong></h1>
<ul>
<li><p>인사이트: MRI or CT 3D recon 이미지 + Touch X 기기를 활용하여 Surgical Robotics Navigation 연구를 진행할 수 있을 것 같습니다.</p>
</li>
<li><p>Ref: <a href="https://ieeexplore.ieee.org/document/10684721">https://ieeexplore.ieee.org/document/10684721</a></p>
</li>
<li><p>Summary: SlicerROS2 is an integrated software combining 3D Slicer and ROS. It initially used the ROS and C++ API from 3D Slicer in its first release. Now, the rewritten and redesigned module enables access to 3D Slicer’s Python API. This open-source library supports image-guided robotic interventions that involve the use of medical imaging in tandem with robotics.</p>
</li>
<li><p>library:</p>
<ul>
<li><a href="https://github.com/rosmed/slicer_ros2_module?tab=readme-ov-file">https://github.com/rosmed/slicer_ros2_module?tab=readme-ov-file</a></li>
<li><a href="https://slicer-ros2.readthedocs.io/">https://slicer-ros2.readthedocs.io/</a></li>
</ul>
</li>
</ul>
<blockquote>
<p>🚀 <strong>Four Applications of SlicerROS2</strong> (with <strong>touch-based feedback)</strong></p>
</blockquote>
<ol>
<li>Surgical Navigation: <strong>Touch X</strong> → prevent the robot from breaching specific anatomical boundaries.</li>
<li><strong>Image-Guided Motion Planning</strong>: <strong>VRK</strong> (da Vinci Research Kit) → plan and simulate surgical paths. </li>
<li><strong>Robot and Image Simulation</strong>: <strong>Gazebo simulator</strong> for robotic ultrasound simulation → Realistic tissue interaction</li>
<li><strong>Custom Device Integration</strong>: <strong>MRI-guided robotic devices</strong> → accurate placement and interaction with MRI images during interventions.</li>
</ol>
<p><img alt="" src="https://velog.velcdn.com/images/yechxn/post/18bae50e-5be9-4ea8-86af-b78417366bd0/image.png" /></p>