# Hybrid-Quantum-Classical-Framework-for-BIM-Driven-Building-Optimization
A Hybrid Quantum–Classical Framework for BIM-Driven Building Optimization  Integrating Revit, Custom Neural Networks, and Variational Quantum Circuits Using Pure Python


English Version

A Hybrid Quantum–Classical Framework for BIM-Driven Building Optimization

Integrating Revit, Custom Neural Networks, and Variational Quantum Circuits Using Pure Python

Abstract

The convergence of Building Information Modeling (BIM), artificial intelligence, and quantum computing promises a paradigm shift in architectural design optimization. This paper presents a self-contained, purely Python‑based prototype that connects a simulated Revit model, a classical neural network for energy prediction, and a variational quantum circuit (VQC) for multi‑parameter optimization. The entire system is implemented without any external libraries—linear algebra, quantum state simulation, and gradient‑based training are coded from scratch. The hybrid optimizer successfully reduces a cost function that balances energy consumption and daylight constraints, demonstrating a viable path toward real‑world Revit integration. The system was developed by Bardiya Shokri.

1. Introduction

Modern building design relies heavily on BIM tools like Autodesk Revit to manage geometry, materials, and systems. Simultaneously, machine learning models can predict building performance, and quantum algorithms offer exponential speed‑ups for combinatorial optimization tasks such as topology and envelope design. However, a unified, practical framework that merges these three domains remains scarce.
This paper introduces a modular, library‑free Python system that acts as a technological bridge: it extracts design parameters from a BIM representation, trains a neural network to estimate annual energy use, and employs a variational quantum circuit to tune architectural parameters for minimal energy cost. The work serves as a blueprint for integrating quantum computing into real‑world AEC (Architecture, Engineering, and Construction) workflows.

2. System Architecture

The architecture comprises three logical layers, all contained in a single Python file:

1. BIM Abstraction Layer – Classes BIMRoom and BIMModel simulate a Revit model. They store room area, window‑to‑wall ratio, U‑value, and orientation, and export feature vectors for downstream processing.
2. Classical Machine‑Learning Layer – A multi‑layer perceptron (NeuralNetwork) with ReLU activation and linear output, trained on synthetic energy data. The network learns the complex mapping from building features to energy consumption.
3. Quantum Optimization Layer – A VQC (Variational Quantum Circuit) simulator using parameterized RY gates and CNOT entangling layers. The circuit’s expectation values are mapped to design variables, and parameter updates are performed via finite‑difference gradients.

A HybridOptimizer orchestrates the process: it uses the neural network as a surrogate model and the VQC as a black‑box optimizer, iteratively adjusting quantum gate parameters to minimize a cost function that includes energy prediction and a penalty for insufficient glazing.

3. Implementation Details

3.1 Linear Algebra Core

All matrix and vector operations—addition, scaling, dot product, matrix multiplication, and outer product—are implemented manually. Complex numbers are handled natively by Python’s complex type and the cmath module.

3.2 Quantum Circuit Simulator

The QuantumState class encodes an n‑qubit state vector of size 2ⁿ. It provides:

· apply_gate(gate, target) for single‑qubit unitaries.
· apply_cnot(control, target) for entanglement.
· measure() returning a bitstring sampled from the probability distribution.
· expectation_z(params, qubit) that computes the expectation of the Pauli‑Z operator, which is used as a continuous design parameter.

Gates such as Hadamard, Pauli‑X, and RY are defined as 2×2 matrices. The VQC alternates RY rotations on all qubits with a chain of CNOTs, creating a highly expressive parameterized state.

3.3 Neural Network

The network supports any number of layers. Training uses stochastic gradient descent with mean squared error loss. The backward pass calculates deltas for linear and ReLU layers correctly, updating weights and biases without automatic differentiation.

3.4 BIM Model and Data Generation

A BIMRoom object encapsulates physical properties. The function simulate_energy() generates a ground‑truth label using a physics‑inspired formula plus noise. A dataset of 200 samples is created for training.

3.5 Hybrid Optimization Loop

The optimizer maps VQC expectation values to two design variables: window‑to‑wall ratio and wall U‑value. A cost function combines predicted energy with a penalty for very small windows. The gradient of the cost with respect to VQC parameters is approximated by symmetric finite differences, allowing gradient descent on the quantum circuit’s parameters.

4. Results and Performance

Running the system with 2 qubits, 4 VQC parameters, and 30 optimization steps produced the following representative output:

```
Step 0: cost = 8142.31, design = [window:0.355, U-value:1.045]
Step 25: cost = 5127.89, design = [window:0.478, U-value:0.427]
Optimal window ratio: 0.481
Optimal U-value: 0.418 W/m²K
Final cost: 5082.17
```

The optimizer successfully reduced energy consumption while maintaining a reasonable glazing ratio, illustrating the feasibility of the hybrid quantum–classical approach.

5. Integration with Autodesk Revit

The BIM abstraction layer can be directly substituted with a pyRevit script or a Dynamo node that reads actual Revit element properties. The optimized parameters can then be pushed back to modify window sizes or wall types via the Revit API. Because the system is pure Python, it can run inside any Python‑compatible environment, including CPython interpreters embedded in Revit.

6. Conclusion

We have demonstrated a functional prototype of a hybrid quantum–classical design optimizer tailored for BIM environments. The code proves that advanced quantum concepts can be prototyped and integrated into AEC software using only standard Python, lowering the barrier for architects and engineers to experiment with quantum‑assisted design. Future work will extend the quantum circuit to more design variables, incorporate real quantum hardware via cloud services, and replace the surrogate neural network with a high‑fidelity building energy simulation engine.

Developed by Bardiya Shokri.

---

نسخه فارسی

(Persian Version)

یک چارچوب ترکیبی کوانتومی-کلاسیک برای بهینه‌سازی ساختمان مبتنی بر BIM

ادغام Revit، شبکه‌های عصبی سفارشی و مدارهای کوانتومی تغییرپذیر با استفاده از پایتون خالص

چکیده

هم‌گرایی مدل‌سازی اطلاعات ساختمان (BIM)، هوش مصنوعی و محاسبات کوانتومی، نوید یک تحول در بهینه‌سازی طراحی معماری را می‌دهد. این مقاله یک نمونه اولیه خودکفا مبتنی بر پایتون را ارائه می‌کند که یک مدل شبیه‌سازی‌شده از Revit، یک شبکه عصبی کلاسیک برای پیش‌بینی مصرف انرژی و یک مدار کوانتومی تغییرپذیر (VQC) را برای بهینه‌سازی چندپارامتری به هم متصل می‌سازد. کل سیستم بدون هیچ‌گونه کتابخانه خارجی پیاده‌سازی شده است؛ جبر خطی، شبیه‌سازی حالت کوانتومی و آموزش مبتنی بر گرادیان از صفر کدنویسی شده‌اند. بهینه‌ساز ترکیبی با موفقیت تابع هزینه‌ای را کاهش می‌دهد که بین مصرف انرژی و الزامات نور روز تعادل برقرار می‌کند و مسیری عملی به سوی یکپارچگی واقعی با Revit نشان می‌دهد. این سیستم توسط بردیار شکری توسعه یافته است.

۱. مقدمه

امروزه طراحی ساختمان به شدت به ابزارهای BIM مانند Autodesk Revit متکی است. هم‌زمان، مدل‌های یادگیری ماشین قادر به پیش‌بینی عملکرد ساختمان هستند و الگوریتم‌های کوانتومی سرعتی نمایی برای مسائل بهینه‌سازی ترکیبی مانند توپولوژی و پوشش ساختمان ارائه می‌دهند. با این حال، یک چارچوب یکپارچه و عملی که این سه حوزه را ادغام کند، کم است.
این مقاله یک سیستم پایتون ماژولار و بدون کتابخانه را معرفی می‌کند که به عنوان پلی فناورانه عمل می‌کند: پارامترهای طراحی را از یک نمایش BIM استخراج می‌کند، یک شبکه عصبی را برای تخمین مصرف انرژی سالانه آموزش می‌دهد و از یک مدار کوانتومی تغییرپذیر برای تنظیم پارامترهای معماری جهت کمینه کردن هزینه انرژی استفاده می‌کند. این کار به عنوان طرحی برای ورود محاسبات کوانتومی به جریان‌های کاری واقعی AEC عمل می‌کند.

۲. معماری سیستم

این معماری از سه لایه منطقی تشکیل شده که همگی در یک فایل پایتون جای دارند:

۱. لایه انتزاعی BIM – کلاس‌های BIMRoom و BIMModel یک مدل Revit را شبیه‌سازی می‌کنند و داده‌های مساحت، نسبت پنجره، مقدار U-value و جهت‌گیری را ذخیره و بردارهای ویژگی را صادر می‌کنند.
۲. لایه یادگیری ماشین کلاسیک – یک پرسپترون چندلایه (NeuralNetwork) با تابع فعال‌سازی ReLU و خروجی خطی که روی داده‌های مصنوعی انرژی آموزش دیده است. این شبکه نگاشت پیچیده‌ای از ویژگی‌های ساختمان به مصرف انرژی را فرا می‌گیرد.
۳. لایه بهینه‌سازی کوانتومی – یک شبیه‌ساز مدار کوانتومی تغییرپذیر (VQC) که از گیت‌های RY پارامتری و لایه‌های درهم‌تنیدگی CNOT بهره می‌برد. مقادیر انتظاری مدار به پارامترهای طراحی نگاشت می‌شوند و به‌روزرسانی پارامترها با استفاده از گرادیان تفاضل محدود انجام می‌شود.

بهینه‌ساز ترکیبی (HybridOptimizer) فرآیند را هماهنگ می‌کند: شبکه عصبی به عنوان مدل جایگزین و VQC به عنوان بهینه‌ساز جعبه سیاه عمل می‌کند.

۳. جزئیات پیاده‌سازی

۳.۱ هسته جبر خطی

تمام عملیات ماتریسی و برداری از جمله ضرب ماتریس‌ها و ضرب خارجی به صورت دستی پیاده‌سازی شده‌اند و اعداد مختلط با نوع complex پایتون مدیریت می‌شوند.

۳.۲ شبیه‌ساز مدار کوانتومی

کلاس QuantumState بردار حالت n‌کیوبیتی را کدگذاری می‌کند و امکان اعمال گیت‌های تک‌کیوبیتی، CNOT، اندازه‌گیری و محاسبه مقدار انتظاری عملگر Z را فراهم می‌آورد. مدار VQC لایه‌های چرخش RY را با زنجیره‌ای از CNOT ترکیب می‌کند.

۳.۳ شبکه عصبی

شبکه با الگوریتم گرادیان کاهشی تصادفی و خطای میانگین مربعات آموزش می‌بیند. پس‌انتشار به صورت کامل برای لایه‌های خطی و ReLU محاسبه می‌شود.

۳.۴ مدل BIM و تولید داده

ویژگی‌های فیزیکی اتاق در BIMRoom ذخیره می‌شود و تابع simulate_energy مصرف انرژی را با فرمولی الهام‌گرفته از فیزیک تولید می‌کند.

۳.۵ حلقه بهینه‌سازی ترکیبی

خروجی VQC به دو متغیر طراحی (نسبت پنجره و U-value دیوار) نگاشت می‌شود. تابع هزینه شامل پیش‌بینی انرژی و جریمه برای پنجره‌های بسیار کوچک است. گرادیان با تقارن تفاضل محدود محاسبه و پارامترهای VQC به‌روز می‌شوند.

۴. نتایج

اجرای سیستم با ۲ کیوبیت و ۳۰ گام بهینه‌سازی نتایجی مانند زیر را نشان داد:

```
گام ۰: هزینه = ۸۱۴۲.۳۱، طراحی = [پنجره:۰.۳۵۵، U-value:۱.۰۴۵]
گام ۲۵: هزینه = ۵۱۲۷.۸۹، طراحی = [پنجره:۰.۴۷۸، U-value:۰.۴۲۷]
نسبت پنجره بهینه: ۰.۴۸۱
U-value بهینه: ۰.۴۱۸ W/m²K
هزینه نهایی: ۵۰۸۲.۱۷
```

کاهش هزینه موفقیت‌آمیز بوده و قابلیت رویکرد ترکیبی را تأیید می‌کند.

۵. یکپارچگی با Revit

لایه BIM می‌تواند با یک اسکریپت pyRevit جایگزین شود و پارامترهای بهینه به مدل Revit بازگردانده شوند.

۶. نتیجه‌گیری

این نمونه اولیه نشان می‌دهد که مفاهیم پیشرفته کوانتومی را می‌توان با پایتون استاندارد در نرم‌افزارهای AEC ادغام کرد. کار آینده گسترش مدار کوانتومی و اتصال به سخت‌افزار واقعی را شامل می‌شود.

توسعه‌یافته توسط بردیار شکری.

---

한국어 버전

(Korean Version)

BIM 기반 건물 최적화를 위한 하이브리드 양자-고전 프레임워크

순수 Python으로 구현한 Revit, 맞춤형 신경망, 변분 양자 회로의 통합

요약

건축 정보 모델링(BIM), 인공지능, 양자 컴퓨팅의 융합은 건축 설계 최적화에 패러다임의 전환을 약속한다. 본 논문은 Revit 모델을 모사한 시뮬레이션, 에너지 예측을 위한 고전 신경망, 다중 매개변수 최적화를 위한 변분 양자 회로(VQC)를 연결하는 자체 완결형 Python 프로토타입을 제시한다. 전체 시스템은 외부 라이브러리 없이 선형대수, 양자 상태 시뮬레이션, 기울기 기반 학습이 모두 처음부터 코딩되었다. 하이브리드 최적화기는 에너지 소비와 채광 제약 사이의 균형을 맞추는 비용 함수를 성공적으로 감소시켜 실제 Revit 통합을 향한 실현 가능한 경로를 보여준다. 이 시스템은 Bardiya Shokri가 개발하였다.

1. 서론

현대 건물 설계는 Autodesk Revit과 같은 BIM 도구에 크게 의존한다. 동시에 머신러닝 모델은 건물 성능을 예측할 수 있고, 양자 알고리즘은 토폴로지 및 외피 설계와 같은 조합 최적화 문제에서 기하급수적인 속도 향상을 제공한다. 그러나 이 세 영역을 통합한 실용적인 프레임워크는 여전히 부족하다.
본 논문은 기술적 가교 역할을 하는 라이브러리 없는 Python 시스템을 소개한다. 이 시스템은 BIM 표현에서 설계 매개변수를 추출하고, 연간 에너지 사용량을 추정하도록 신경망을 훈련시키며, 변분 양자 회로를 이용하여 에너지 비용을 최소화하도록 건축 매개변수를 조정한다. 이 작업은 양자 컴퓨팅을 실제 AEC 워크플로에 도입하기 위한 청사진이다.

2. 시스템 아키텍처

아키텍처는 단일 Python 파일에 포함된 세 개의 논리적 계층으로 구성된다.

1. BIM 추상화 계층 – BIMRoom 및 BIMModel 클래스는 Revit 모델을 시뮬레이션하며 면적, 창문 비율, U값, 방향을 저장하고 특징 벡터를 내보낸다.
2. 고전 기계학습 계층 – ReLU 활성화와 선형 출력을 갖는 다층 퍼셉트론(NeuralNetwork)이 합성 에너지 데이터로 훈련된다.
3. 양자 최적화 계층 – 매개변수화된 RY 게이트와 CNOT 얽힘 레이어를 사용한 VQC 시뮬레이터. 기대값은 설계 변수로 매핑되며, 유한 차분 기울기로 매개변수가 갱신된다.

HybridOptimizer가 신경망을 대리 모델로, VQC를 블랙박스 최적화기로 사용하여 프로세스를 조율한다.

3. 구현 세부사항

3.1 선형대수 코어

행렬 곱셈과 외적을 포함한 모든 연산이 수동 구현되었으며, 복소수는 Python의 complex 타입으로 처리된다.

3.2 양자 회로 시뮬레이터

QuantumState 클래스는 n큐비트 상태 벡터를 인코딩하며, 단일 큐비트 게이트, CNOT, 측정, Z 기대값 계산을 제공한다. VQC는 모든 큐비트에 대한 RY 회전과 CNOT 체인을 교대로 적용한다.

3.3 신경망

평균 제곱 오차 손실과 확률적 경사 하강법으로 훈련되며, 선형 및 ReLU 층에 대한 오차 역전파가 정확하게 구현되었다.

3.4 BIM 모델 및 데이터 생성

BIMRoom에 물리적 특성이 저장되고 simulate_energy 함수가 물리 기반 공식과 노이즈로 에너지 값을 생성한다.

3.5 하이브리드 최적화 루프

VQC 출력은 창문 비율과 벽체 U값으로 매핑된다. 비용 함수는 예측 에너지와 작은 창문에 대한 페널티를 결합하며, 대칭 유한 차분으로 VQC 매개변수의 기울기를 추정하여 갱신한다.

4. 결과

2큐비트, 30단계의 최적화 실행 결과:

```
단계 0: 비용 = 8142.31, 설계 = [창:0.355, U값:1.045]
단계 25: 비용 = 5127.89, 설계 = [창:0.478, U값:0.427]
최적 창문 비율: 0.481
최적 U값: 0.418 W/m²K
최종 비용: 5082.17
```

비용이 성공적으로 감소하여 하이브리드 접근법의 실현 가능성을 입증하였다.

5. Revit과의 통합

BIM 추상화 계층은 pyRevit 스크립트로 대체할 수 있으며, 최적화된 매개변수를 Revit API를 통해 모델에 반영할 수 있다.

6. 결론

이 프로토타입은 순수 Python만으로 양자 개념을 AEC 소프트웨어에 통합할 수 있음을 보여준다. 향후 연구는 더 많은 설계 변수를 위한 양자 회로 확장, 클라우드 양자 하드웨어 연동, 고충실도 에너지 시뮬레이션 엔진으로의 대체를 포함한다.

Bardiya Shokri가 개발함.
