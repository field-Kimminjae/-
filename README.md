<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>컴퓨터 구매 초보자 가이드</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <link href="https://fonts.googleapis.com/css2?family=Noto+Sans+KR:wght@300;400;500;700&display=swap" rel="stylesheet">
    <!-- Chosen Palette: Warm Neutrals with Blue Accent -->
    <!-- Application Structure Plan: A 4-step guided journey for the user. 1. Select Use Case (sets the context). 2. Explore Recommended Build (interactive diagram). 3. Deep Dive & Compare Components (interactive charts). 4. Buyer's Checklist (actionable advice). This task-oriented structure is more intuitive for beginners than a linear report, guiding them from their primary need to detailed information and finally to purchasing advice, making the complex topic digestible and engaging. -->
    <!-- Visualization & Content Choices: Use case selection via buttons (Goal: Filter, Method: JS state change) for immediate personalization. Interactive component diagram (Goal: Organize, Method: HTML/CSS) to visually map components. Dynamic bar/radar charts via Chart.js (Goal: Compare, Method: Canvas) to make data from tables (e.g., SSD vs HDD) more intuitive. Accordion for the checklist (Goal: Organize, Method: JS toggle) to manage text density. This combination supports the guided structure by providing information on demand. -->
    <!-- CONFIRMATION: NO SVG graphics used. NO Mermaid JS used. -->
    <style>
        body {
            font-family: 'Noto Sans KR', sans-serif;
        }
        .chart-container {
            position: relative;
            width: 100%;
            max-width: 600px;
            margin-left: auto;
            margin-right: auto;
            height: 300px;
            max-height: 400px;
        }
        @media (min-width: 768px) {
            .chart-container {
                height: 350px;
            }
        }
        .nav-button.active {
            background-color: #3B82F6;
            color: white;
            font-weight: 700;
        }
        .component-card {
            transition: all 0.3s ease-in-out;
            cursor: pointer;
        }
        .component-card:hover {
            transform: translateY(-5px);
            box-shadow: 0 10px 15px -3px rgb(0 0 0 / 0.1), 0 4px 6px -4px rgb(0 0 0 / 0.1);
        }
        .accordion-content {
            max-height: 0;
            overflow: hidden;
            transition: max-height 0.3s ease-out;
        }
    </style>
</head>
<body class="bg-stone-100 text-gray-800">

    <div class="container mx-auto p-4 md:p-8">

        <header class="text-center mb-12">
            <h1 class="text-4xl md:text-5xl font-bold text-blue-600 mb-4">첫 컴퓨터 구매, 성공을 위한 안내서</h1>
            <p class="text-lg text-gray-600">복잡한 컴퓨터의 세계, 당신의 용도에 맞춰 쉽고 명확하게 길을 안내해 드립니다.</p>
        </header>

        <main>
            <!-- Step 1: Use Case Selection -->
            <section id="step1" class="mb-12 bg-white p-8 rounded-xl shadow-md">
                <h2 class="text-2xl font-bold mb-2 text-center">Step 1. 당신의 컴퓨터, 어떤 용도로 사용하실 건가요?</h2>
                <p class="text-center text-gray-600 mb-6">가장 주된 사용 목적을 선택하시면, 그에 맞는 최적의 사양을 추천해 드립니다.</p>
                <div id="useCaseSelector" class="flex flex-col sm:flex-row justify-center gap-4">
                    <button data-usecase="office" class="nav-button w-full sm:w-auto text-lg px-8 py-4 bg-white border-2 border-blue-500 text-blue-500 rounded-lg shadow-sm hover:bg-blue-50 transition duration-300">
                        <span class="text-2xl">📑</span><br>문서 & 웹서핑
                    </button>
                    <button data-usecase="multimedia" class="nav-button w-full sm:w-auto text-lg px-8 py-4 bg-white border-2 border-blue-500 text-blue-500 rounded-lg shadow-sm hover:bg-blue-50 transition duration-300">
                        <span class="text-2xl">🎮</span><br>가벼운 게임 & 미디어
                    </button>
                    <button data-usecase="professional" class="nav-button w-full sm:w-auto text-lg px-8 py-4 bg-white border-2 border-blue-500 text-blue-500 rounded-lg shadow-sm hover:bg-blue-50 transition duration-300">
                        <span class="text-2xl">🎬</span><br>고사양 게임 & 전문 작업
                    </button>
                </div>
            </section>

            <!-- Step 2: Recommended Build -->
            <section id="step2" class="mb-12 hidden">
                <h2 class="text-2xl font-bold mb-2 text-center">Step 2. 당신을 위한 추천 컴퓨터 사양</h2>
                <p class="text-center text-gray-600 mb-6">각 부품을 클릭하여 역할과 추천 사양에 대한 설명을 확인해 보세요.</p>
                <div class="bg-white p-6 md:p-8 rounded-xl shadow-md">
                    <div class="grid grid-cols-2 lg:grid-cols-3 gap-4 md:gap-6 text-center">
                        <div data-component="cpu" class="component-card bg-stone-50 p-6 rounded-lg border border-gray-200">
                            <h3 class="font-bold text-xl mb-1">CPU 🧠</h3>
                            <p class="text-gray-500 text-sm mb-2">컴퓨터의 두뇌</p>
                            <p id="rec-cpu" class="font-semibold text-blue-600"></p>
                        </div>
                        <div data-component="ram" class="component-card bg-stone-50 p-6 rounded-lg border border-gray-200">
                            <h3 class="font-bold text-xl mb-1">RAM ✍️</h3>
                            <p class="text-gray-500 text-sm mb-2">작업 공간</p>
                            <p id="rec-ram" class="font-semibold text-blue-600"></p>
                        </div>
                        <div data-component="storage" class="component-card bg-stone-50 p-6 rounded-lg border border-gray-200">
                            <h3 class="font-bold text-xl mb-1">저장장치 💾</h3>
                            <p class="text-gray-500 text-sm mb-2">데이터 저장소</p>
                            <p id="rec-storage" class="font-semibold text-blue-600"></p>
                        </div>
                        <div data-component="gpu" class="component-card bg-stone-50 p-6 rounded-lg border border-gray-200">
                            <h3 class="font-bold text-xl mb-1">GPU 🎨</h3>
                            <p class="text-gray-500 text-sm mb-2">그래픽 처리</p>
                            <p id="rec-gpu" class="font-semibold text-blue-600"></p>
                        </div>
                        <div data-component="motherboard" class="component-card bg-stone-50 p-6 rounded-lg border border-gray-200">
                            <h3 class="font-bold text-xl mb-1">메인보드 🔗</h3>
                            <p class="text-gray-500 text-sm mb-2">모든 부품의 연결</p>
                             <p class="font-semibold text-gray-600">안정성/호환성</p>
                        </div>
                        <div data-component="psu" class="component-card bg-stone-50 p-6 rounded-lg border border-gray-200">
                            <h3 class="font-bold text-xl mb-1">파워 ⚡</h3>
                            <p class="text-gray-500 text-sm mb-2">안정적인 전력</p>
                             <p class="font-semibold text-gray-600">시스템 안정성</p>
                        </div>
                    </div>
                </div>
            </section>
            
            <!-- Modal for component details -->
            <div id="componentModal" class="fixed inset-0 bg-black bg-opacity-50 hidden items-center justify-center p-4 z-50">
                <div class="bg-white rounded-lg shadow-xl w-full max-w-lg p-6 relative">
                    <button id="closeModal" class="absolute top-4 right-4 text-gray-500 hover:text-gray-800 text-2xl">&times;</button>
                    <h3 id="modalTitle" class="text-2xl font-bold mb-4"></h3>
                    <p id="modalDescription" class="text-gray-700 mb-4"></p>
                    <div class="bg-blue-50 p-4 rounded-md">
                        <h4 class="font-semibold text-blue-800">추천 사양 (<span id="modalUseCase"></span>)</h4>
                        <p id="modalRecommendation" class="text-blue-700"></p>
                    </div>
                </div>
            </div>

            <!-- Step 3: Deep Dive -->
            <section id="step3" class="mb-12 hidden">
                <h2 class="text-2xl font-bold mb-2 text-center">Step 3. 주요 부품, 차트로 비교하기</h2>
                <p class="text-center text-gray-600 mb-6">부품별 성능 차이를 차트를 통해 한눈에 파악해 보세요.</p>
                <div class="bg-white p-6 md:p-8 rounded-xl shadow-md">
                    <div class="border-b border-gray-200 mb-6">
                        <nav id="deepDiveNav" class="-mb-px flex justify-center space-x-2 md:space-x-8" aria-label="Tabs">
                            <button data-target="compare-cpu" class="deep-dive-tab whitespace-nowrap py-4 px-1 border-b-2 font-medium text-lg border-transparent text-gray-500 hover:text-gray-700 hover:border-gray-300">CPU</button>
                            <button data-target="compare-storage" class="deep-dive-tab whitespace-nowrap py-4 px-1 border-b-2 font-medium text-lg border-transparent text-gray-500 hover:text-gray-700 hover:border-gray-300">저장장치</button>
                            <button data-target="compare-ram" class="deep-dive-tab whitespace-nowrap py-4 px-1 border-b-2 font-medium text-lg border-transparent text-gray-500 hover:text-gray-700 hover:border-gray-300">RAM</button>
                            <button data-target="compare-gpu" class="deep-dive-tab whitespace-nowrap py-4 px-1 border-b-2 font-medium text-lg border-transparent text-gray-500 hover:text-gray-700 hover:border-gray-300">GPU</button>
                        </nav>
                    </div>
                    <div id="compare-cpu" class="deep-dive-content hidden">
                        <h3 class="text-xl font-semibold text-center mb-4">CPU 성능 비교 (코어와 클럭)</h3>
                        <p class="text-center text-gray-600 mb-4">코어 수는 멀티태스킹, 클럭 속도는 단일 작업 속도에 영향을 줍니다. 용도에 맞는 균형이 중요합니다.</p>
                        <div class="chart-container"><canvas id="cpuChart"></canvas></div>
                    </div>
                    <div id="compare-storage" class="deep-dive-content hidden">
                        <h3 class="text-xl font-semibold text-center mb-4">저장장치 비교 (SSD vs HDD)</h3>
                         <p class="text-center text-gray-600 mb-4">SSD는 속도가 매우 빠르고, HDD는 용량 대비 가격이 저렴합니다. 대부분의 경우 SSD가 체감 성능을 크게 향상시킵니다.</p>
                        <div class="chart-container"><canvas id="storageChart"></canvas></div>
                    </div>
                    <div id="compare-ram" class="deep-dive-content hidden">
                         <h3 class="text-xl font-semibold text-center mb-4">RAM 용량별 체감 성능</h3>
                         <p class="text-center text-gray-600 mb-4">RAM 용량이 클수록 여러 프로그램을 동시에 원활하게 실행할 수 있습니다.</p>
                        <div class="chart-container"><canvas id="ramChart"></canvas></div>
                    </div>
                    <div id="compare-gpu" class="deep-dive-content hidden">
                        <h3 class="text-xl font-semibold text-center mb-4">GPU 등급별 성능</h3>
                        <p class="text-center text-gray-600 mb-4">내장 그래픽은 기본 작업용, 외장 그래픽은 게임 및 전문 작업용입니다. 숫자가 높을수록 고성능입니다.</p>
                        <div class="chart-container"><canvas id="gpuChart"></canvas></div>
                    </div>
                </div>
            </section>

            <!-- Step 4: Buyer's Checklist -->
            <section id="step4" class="hidden">
                 <h2 class="text-2xl font-bold mb-2 text-center">Step 4. 사기 방지! 현명한 구매를 위한 체크리스트</h2>
                 <p class="text-center text-gray-600 mb-6">구매 전부터 수령 후까지, 아래 항목들을 확인하여 안전하게 구매하세요.</p>
                <div id="accordion" class="space-y-4">
                     <div class="bg-white rounded-lg shadow-md">
                        <button class="accordion-header w-full flex justify-between items-center text-left p-5 font-semibold text-xl">
                            <span>✅ 신뢰할 수 있는 구매처 선택</span>
                            <span class="accordion-icon transform rotate-0 transition-transform duration-300">+</span>
                        </button>
                        <div class="accordion-content px-5 pb-5 text-gray-700">
                           <ul class="list-disc list-inside space-y-2 mt-2">
                               <li><b>공식 브랜드 스토어:</b> 삼성, LG, HP, Dell 등 제조사 공식몰이 가장 안전합니다.</li>
                               <li><b>대형 전자제품 판매점:</b> 하이마트, 전자랜드 등 직접 보고 상담받을 수 있습니다.</li>
                               <li><b>평판 좋은 온라인 쇼핑몰:</b> 컴퓨존, 다나와, 쿠팡 등 후기가 많고 검증된 곳을 이용하세요.</li>
                               <li><b>주의할 곳:</b> 지나치게 저렴한 가격, 정보가 불분명한 개인 판매자는 피하는 것이 좋습니다.</li>
                           </ul>
                        </div>
                    </div>
                     <div class="bg-white rounded-lg shadow-md">
                        <button class="accordion-header w-full flex justify-between items-center text-left p-5 font-semibold text-xl">
                            <span>📋 구매 전 반드시 확인할 사항</span>
                             <span class="accordion-icon transform rotate-0 transition-transform duration-300">+</span>
                        </button>
                        <div class="accordion-content px-5 pb-5 text-gray-700">
                             <ul class="list-disc list-inside space-y-2 mt-2">
                                <li><b>사양 꼼꼼히 확인:</b> 광고 문구에 현혹되지 말고 CPU, RAM, SSD 등 부품의 정확한 모델명을 확인하세요.</li>
                                <li><b>정품 여부 및 보증 기간:</b> 중고나 비정품 부품 사기에 주의하고, A/S 기간을 꼭 확인하세요.</li>
                                <li><b>환불/교환 규정:</b> 초기 불량에 대비해 환불 및 교환 규정을 미리 읽어보세요. '환불 불가'는 법적 효력이 없는 경우가 많습니다.</li>
                                <li><b>안전 결제:</b> 문제 발생 시 '차지백' 서비스가 가능한 신용카드 결제가 더 안전합니다.</li>
                            </ul>
                        </div>
                    </div>
                    <div class="bg-white rounded-lg shadow-md">
                        <button class="accordion-header w-full flex justify-between items-center text-left p-5 font-semibold text-xl">
                            <span>💻 컴퓨터 수령 후 사양 확인 방법</span>
                             <span class="accordion-icon transform rotate-0 transition-transform duration-300">+</span>
                        </button>
                        <div class="accordion-content px-5 pb-5 text-gray-700">
                            <p>주문한 사양과 실제 제품이 일치하는지 반드시 검증해야 합니다.</p>
                             <ul class="list-disc list-inside space-y-2 mt-2">
                                <li><b>윈도우 내장 기능:</b> [설정 > 시스템 > 정보] 또는 [내 PC 우클릭 > 속성]에서 CPU, RAM 확인. [장치 관리자 > 디스플레이 어댑터]에서 그래픽카드 확인.</li>
                                <li><b>무료 전문 프로그램 활용:</b>
                                    <ul class="list-inside list-disc ml-4">
                                        <li><b>CPU-Z:</b> CPU, 메인보드, RAM 등 핵심 부품 상세 정보 확인</li>
                                        <li><b>GPU-Z:</b> 그래픽카드 상세 정보 확인</li>
                                        <li><b>HWMonitor:</b> 부품별 온도, 전압 등 실시간 상태 확인</li>
                                    </ul>
                                </li>
                           </ul>
                        </div>
                    </div>
                </div>
            </section>
        </main>
    </div>

    <script>
        document.addEventListener('DOMContentLoaded', function () {
            const data = {
                recommendations: {
                    office: {
                        cpu: "인텔 i3 / AMD 라이젠 3 이상",
                        ram: "8GB 이상",
                        storage: "SSD 256GB 이상",
                        gpu: "내장 그래픽",
                        useCaseText: "문서/웹서핑"
                    },
                    multimedia: {
                        cpu: "인텔 i5 / AMD 라이젠 5 이상",
                        ram: "16GB 이상",
                        storage: "SSD 512GB 이상",
                        gpu: "NVIDIA GTX 1660 이상",
                        useCaseText: "가벼운 게임/미디어"
                    },
                    professional: {
                        cpu: "인텔 i7 / AMD 라이젠 7 이상",
                        ram: "32GB 이상",
                        storage: "NVMe SSD 1TB + HDD",
                        gpu: "NVIDIA RTX 3060 이상",
                        useCaseText: "고사양 게임/전문 작업"
                    }
                },
                componentDetails: {
                    cpu: { title: "CPU (중앙처리장치) 🧠", description: "컴퓨터의 '두뇌'로, 모든 계산과 명령어 처리를 담당합니다. CPU의 성능이 컴퓨터의 전반적인 반응 속도를 결정합니다." },
                    ram: { title: "RAM (메모리) ✍️", description: "프로그램 실행 시 필요한 데이터를 임시로 저장하는 '작업 공간'입니다. RAM이 클수록 여러 프로그램을 동시에 원활하게 실행할 수 있습니다." },
                    storage: { title: "저장장치 (SSD/HDD) 💾", description: "운영체제, 프로그램, 개인 파일을 영구적으로 보관하는 '데이터 저장소'입니다. SSD는 부팅과 로딩 속도를 획기적으로 향상시킵니다." },
                    gpu: { title: "GPU (그래픽 카드) 🎨", description: "게임, 영상 편집 등 그래픽과 관련된 복잡한 연산을 전문적으로 처리합니다. 고사양 작업일수록 중요도가 높아집니다." },
                    motherboard: { title: "메인보드 🔗", description: "모든 부품을 연결하고 서로 통신하게 하는 '신경계'와 같습니다. 시스템의 안정성과 확장성을 결정합니다." },
                    psu: { title: "파워 서플라이 ⚡", description: "컴퓨터의 모든 부품에 안정적인 전력을 공급하는 '심장'입니다. 좋은 파워는 부품 수명 연장에 기여합니다." }
                }
            };
            
            let currentUserCase = 'office';
            let charts = {};

            const useCaseSelector = document.getElementById('useCaseSelector');
            const step2 = document.getElementById('step2');
            const step3 = document.getElementById('step3');
            const step4 = document.getElementById('step4');

            const modal = document.getElementById('componentModal');
            const closeModalBtn = document.getElementById('closeModal');

            useCaseSelector.addEventListener('click', function (e) {
                const button = e.target.closest('button');
                if (!button) return;

                currentUserCase = button.dataset.usecase;

                // Update nav buttons UI
                useCaseSelector.querySelectorAll('button').forEach(btn => btn.classList.remove('active'));
                button.classList.add('active');

                // Update recommendations in Step 2
                updateRecommendations(currentUserCase);
                
                // Show subsequent steps
                step2.classList.remove('hidden');
                step3.classList.remove('hidden');
                step4.classList.remove('hidden');

                // Activate first tab in deep dive and update charts
                document.querySelector('.deep-dive-tab').click();
            });

            function updateRecommendations(useCase) {
                const rec = data.recommendations[useCase];
                document.getElementById('rec-cpu').textContent = rec.cpu;
                document.getElementById('rec-ram').textContent = rec.ram;
                document.getElementById('rec-storage').textContent = rec.storage;
                document.getElementById('rec-gpu').textContent = rec.gpu;
            }
            
            step2.addEventListener('click', function(e){
                const card = e.target.closest('.component-card');
                if (!card) return;
                
                const componentKey = card.dataset.component;
                const details = data.componentDetails[componentKey];
                
                document.getElementById('modalTitle').textContent = details.title;
                document.getElementById('modalDescription').textContent = details.description;
                
                const rec = data.recommendations[currentUserCase];
                document.getElementById('modalUseCase').textContent = rec.useCaseText;
                
                let recommendationText = '사양 정보 없음';
                if(rec[componentKey]){
                    recommendationText = rec[componentKey];
                } else {
                     recommendationText = '선택한 용도에 맞는 부품을 선택하세요.';
                }
                
                document.getElementById('modalRecommendation').textContent = recommendationText;

                modal.classList.remove('hidden');
                modal.classList.add('flex');
            });
            
            closeModalBtn.addEventListener('click', () => {
                 modal.classList.add('hidden');
                 modal.classList.remove('flex');
            });
            
            modal.addEventListener('click', (e) => {
                if(e.target === modal) {
                    modal.classList.add('hidden');
                    modal.classList.remove('flex');
                }
            });

            // Deep Dive Tabs
            const deepDiveNav = document.getElementById('deepDiveNav');
            const deepDiveContents = document.querySelectorAll('.deep-dive-content');

            deepDiveNav.addEventListener('click', function(e){
                const button = e.target.closest('button');
                if(!button) return;
                
                deepDiveNav.querySelectorAll('button').forEach(btn => {
                    btn.classList.remove('border-blue-500', 'text-blue-600');
                    btn.classList.add('border-transparent', 'text-gray-500');
                });
                button.classList.add('border-blue-500', 'text-blue-600');
                button.classList.remove('border-transparent', 'text-gray-500');

                deepDiveContents.forEach(content => content.classList.add('hidden'));
                
                const targetContent = document.getElementById(button.dataset.target);
                targetContent.classList.remove('hidden');

                // Load chart
                loadChart(button.dataset.target);
            });

            // Accordion
            document.getElementById('accordion').addEventListener('click', function (e) {
                const header = e.target.closest('.accordion-header');
                if (!header) return;

                const content = header.nextElementSibling;
                const icon = header.querySelector('.accordion-icon');
                
                if (content.style.maxHeight) {
                    content.style.maxHeight = null;
                    icon.classList.remove('rotate-45');
                } else {
                    document.querySelectorAll('.accordion-content').forEach(c => c.style.maxHeight = null);
                    document.querySelectorAll('.accordion-icon').forEach(i => i.classList.remove('rotate-45'));
                    content.style.maxHeight = content.scrollHeight + "px";
                    icon.classList.add('rotate-45');
                }
            });


            function loadChart(chartId) {
                if (charts[chartId]) {
                    charts[chartId].destroy();
                }

                const ctx = document.getElementById(chartId.replace('compare-', '') + 'Chart').getContext('2d');
                let chartConfig;

                switch (chartId) {
                    case 'compare-cpu':
                        chartConfig = getCpuChartConfig();
                        break;
                    case 'compare-storage':
                        chartConfig = getStorageChartConfig();
                        break;
                    case 'compare-ram':
                        chartConfig = getRamChartConfig();
                        break;
                    case 'compare-gpu':
                        chartConfig = getGpuChartConfig();
                        break;
                }
                
                if (chartConfig) {
                    charts[chartId] = new Chart(ctx, chartConfig);
                }
            }

            function getCpuChartConfig() {
                const useCaseData = {
                    office: [30, 20],
                    multimedia: [60, 50],
                    professional: [90, 100]
                };
                return {
                    type: 'bar',
                    data: {
                        labels: ['단일 작업 성능 (클럭)', '멀티태스킹 성능 (코어)'],
                        datasets: [{
                            label: '권장 성능 수준',
                            data: useCaseData[currentUserCase],
                            backgroundColor: ['rgba(59, 130, 246, 0.6)', 'rgba(23, 165, 206, 0.6)'],
                            borderColor: ['rgba(59, 130, 246, 1)', 'rgba(23, 165, 206, 1)'],
                            borderWidth: 1
                        }]
                    },
                    options: {
                        responsive: true,
                        maintainAspectRatio: false,
                        scales: { y: { beginAtZero: true, max: 100 } },
                        plugins: { legend: { display: false }, title: { display: true, text: `${data.recommendations[currentUserCase].useCaseText} 용도` } }
                    }
                };
            }
            
            function getStorageChartConfig() {
                 return {
                    type: 'radar',
                    data: {
                        labels: ['속도', '내구성', '소음', '가격 (저렴)', '용량 (대용량)'],
                        datasets: [
                            {
                                label: 'SSD',
                                data: [95, 85, 100, 40, 60],
                                fill: true,
                                backgroundColor: 'rgba(59, 130, 246, 0.2)',
                                borderColor: 'rgb(59, 130, 246)',
                                pointBackgroundColor: 'rgb(59, 130, 246)',
                            }, {
                                label: 'HDD',
                                data: [30, 60, 50, 90, 95],
                                fill: true,
                                backgroundColor: 'rgba(255, 99, 132, 0.2)',
                                borderColor: 'rgb(255, 99, 132)',
                                pointBackgroundColor: 'rgb(255, 99, 132)',
                            }
                        ]
                    },
                    options: {
                        responsive: true,
                        maintainAspectRatio: false,
                        scales: { r: { beginAtZero: true, max: 100 } }
                    }
                };
            }

            function getRamChartConfig() {
                 const useCaseData = {
                    office: [80, 20, 0],
                    multimedia: [40, 90, 30],
                    professional: [10, 50, 95]
                };
                return {
                    type: 'bar',
                    data: {
                        labels: ['8GB', '16GB', '32GB 이상'],
                        datasets: [{
                            label: '작업 원활도',
                            data: useCaseData[currentUserCase],
                            backgroundColor: ['rgba(255, 205, 86, 0.6)', 'rgba(75, 192, 192, 0.6)', 'rgba(54, 162, 235, 0.6)'],
                            borderColor: ['rgb(255, 205, 86)', 'rgb(75, 192, 192)', 'rgb(54, 162, 235)'],
                            borderWidth: 1
                        }]
                    },
                    options: {
                        indexAxis: 'y',
                        responsive: true,
                        maintainAspectRatio: false,
                        scales: { x: { beginAtZero: true, max: 100 } },
                        plugins: { legend: { display: false }, title: { display: true, text: `${data.recommendations[currentUserCase].useCaseText} 용도` } }
                    }
                };
            }

            function getGpuChartConfig() {
                const useCaseData = {
                    office: [100, 10, 0],
                    multimedia: [50, 100, 40],
                    professional: [10, 60, 100]
                };
                 return {
                    type: 'bar',
                    data: {
                        labels: ['내장 그래픽', '보급형 외장 (GTX 16급)', '고성능 외장 (RTX 30급 이상)'],
                        datasets: [{
                            label: '성능 적합도',
                            data: useCaseData[currentUserCase],
                            backgroundColor: ['rgba(255, 159, 64, 0.6)', 'rgba(153, 102, 255, 0.6)', 'rgba(255, 99, 132, 0.6)'],
                            borderColor: ['rgb(255, 159, 64)', 'rgb(153, 102, 255)', 'rgb(255, 99, 132)'],
                            borderWidth: 1
                        }]
                    },
                    options: {
                        responsive: true,
                        maintainAspectRatio: false,
                        scales: { y: { beginAtZero: true, max: 100 } },
                        plugins: { legend: { display: false }, title: { display: true, text: `${data.recommendations[currentUserCase].useCaseText} 용도` } }
                    }
                };
            }

            // Set initial state
            document.querySelector('[data-usecase="office"]').click();
        });
    </script>
</body>
</html>
