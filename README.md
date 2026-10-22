<!DOCTYPE html>
<html lang="ko">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>라드매치 (RadMatch) | 방사선사 전용 대진·알바 매칭 플랫폼</title>
  
  <!-- Pretendard Korean Font -->
  <link rel="stylesheet" as="style" crossorigin href="https://cdn.jsdelivr.net/gh/orioncactus/pretendard@v1.3.9/dist/web/static/pretendard.css" />
  
  <!-- Tailwind CSS CDN -->
  <script src="https://cdn.tailwindcss.com"></script>
  
  <!-- Lucide Icons CDN -->
  <script src="https://unpkg.com/lucide@latest"></script>

  <script>
    tailwind.config = {
      theme: {
        extend: {
          fontFamily: {
            sans: ['Pretendard', '-apple-system', 'BlinkMacSystemFont', 'system-ui', 'Roboto', 'sans-serif'],
          },
          colors: {
            brand: {
              50: '#ecfeff',
              100: '#cffafe',
              200: '#a5f3fc',
              300: '#67e8f9',
              400: '#22d3ee',
              500: '#06b6d4',
              600: '#0891b2',
              700: '#0e7490',
              800: '#155e75',
              900: '#164e63',
              950: '#083344',
            },
            medical: {
              blue: '#0284c7',
              navy: '#0f172a',
              teal: '#0d9488',
              emerald: '#059669',
            }
          }
        }
      }
    }
  </script>

  <style>
    /* Custom scrollbar */
    ::-webkit-scrollbar {
      width: 6px;
      height: 6px;
    }
    ::-webkit-scrollbar-track {
      background: #f1f5f9;
    }
    ::-webkit-scrollbar-thumb {
      background: #cbd5e1;
      border-radius: 9999px;
    }
    ::-webkit-scrollbar-thumb:hover {
      background: #94a3b8;
    }
    
    /* Smooth transitions */
    .modal-backdrop {
      background-color: rgba(15, 23, 42, 0.65);
      backdrop-filter: blur(4px);
    }
  </style>
</head>
<body class="bg-slate-50 text-slate-800 antialiased min-h-screen flex flex-col font-sans">

  <!-- Header -->
  <header class="sticky top-0 z-40 bg-white/95 backdrop-blur border-b border-slate-200 shadow-sm">
    <div class="max-w-6xl mx-auto px-4 h-16 flex items-center justify-between">
      <!-- Logo -->
      <a href="#" class="flex items-center gap-2.5 group">
        <div class="w-10 h-10 rounded-xl bg-gradient-to-tr from-brand-700 to-cyan-500 flex items-center justify-center text-white shadow-md shadow-brand-500/20 group-hover:scale-105 transition-transform">
          <i data-lucide="scan-line" class="w-6 h-6"></i>
        </div>
        <div>
          <div class="flex items-center gap-1.5">
            <span class="text-xl font-black tracking-tight text-slate-900">라드매치</span>
            <span class="text-[10px] font-bold px-1.5 py-0.5 rounded bg-brand-50 text-brand-700 border border-brand-200">방사선사 전용</span>
          </div>
          <p class="text-[11px] text-slate-500 -mt-1 font-medium">대한민국 No.1 영상의학 대진·알바</p>
        </div>
      </a>

      <!-- Quick Nav Buttons -->
      <div class="flex items-center gap-2">
        <button onclick="openPostModal()" class="hidden sm:inline-flex items-center gap-1.5 bg-slate-900 hover:bg-slate-800 text-white text-xs font-semibold px-3.5 py-2 rounded-lg shadow transition">
          <i data-lucide="plus-circle" class="w-4 h-4 text-brand-400"></i>
          <span>대진/구인 공고 등록</span>
        </button>
        
        <button onclick="openProfileModal()" class="inline-flex items-center gap-1.5 bg-slate-100 hover:bg-slate-200 text-slate-700 text-xs font-semibold px-3 py-2 rounded-lg transition relative">
          <i data-lucide="user-check" class="w-4 h-4 text-slate-600"></i>
          <span class="hidden xs:inline">내 프로필 & 지원현황</span>
          <span id="headerAppliedBadge" class="hidden absolute -top-1 -right-1 bg-brand-600 text-white text-[10px] w-4 h-4 rounded-full flex items-center justify-center font-bold">0</span>
        </button>
      </div>
    </div>
  </header>

  <!-- Hero Section & Key Metric -->
  <section class="bg-gradient-to-b from-slate-900 via-slate-800 to-slate-900 text-white pt-8 pb-12 px-4 relative overflow-hidden">
    <!-- Background glow -->
    <div class="absolute -top-24 left-1/2 -translate-x-1/2 w-96 h-96 bg-brand-500/20 rounded-full blur-3xl pointer-events-none"></div>

    <div class="max-w-5xl mx-auto relative z-10 text-center">
      <div class="inline-flex items-center gap-2 px-3 py-1 rounded-full bg-brand-950/80 border border-brand-500/30 text-brand-300 text-xs font-medium mb-4">
        <span class="w-2 h-2 rounded-full bg-emerald-400 animate-pulse"></span>
        <span>실시간 C-arm / 일반촬영 / CT 대진 매칭 중</span>
      </div>

      <h1 class="text-2xl sm:text-4xl font-extrabold tracking-tight text-white mb-3">
        원하는 날짜, 검증된 병원, <span class="text-transparent bg-clip-text bg-gradient-to-r from-brand-300 to-cyan-400">당일 지급 대진 알바</span>
      </h1>
      <p class="text-xs sm:text-base text-slate-300 max-w-2xl mx-auto mb-8 font-light leading-relaxed">
        정형외과 C-arm, 종합병원 CT/MRI 당직, 검진센터 맘모·BMD까지!<br class="hidden sm:inline">
        방사선사 면허 소지자를 위한 믿을 수 있는 구인구직 직거래 플랫폼
      </p>

      <!-- Search Bar -->
      <div class="max-w-2xl mx-auto bg-white p-2 rounded-2xl shadow-xl flex flex-col sm:flex-row gap-2 text-slate-800">
        <div class="flex-1 flex items-center px-3 gap-2">
          <i data-lucide="search" class="w-5 h-5 text-slate-400"></i>
          <input 
            type="text" 
            id="searchInput" 
            placeholder="병원명, 지역(강남, 수원 등), 장비(C-arm, CT 등) 검색..." 
            class="w-full py-2 text-sm text-slate-800 placeholder-slate-400 focus:outline-none"
            oninput="handleSearch()"
          >
        </div>
        <div class="flex items-center gap-1.5 border-t sm:border-t-0 sm:border-l border-slate-100 pt-2 sm:pt-0 sm:pl-2">
          <select id="regionFilter" onchange="applyFilters()" class="text-xs bg-slate-50 border border-slate-200 text-slate-700 py-2.5 px-3 rounded-xl focus:outline-none focus:ring-1 focus:ring-brand-500">
            <option value="all">전체 지역</option>
            <option value="서울">서울 전체</option>
            <option value="강남/서초/송파">서울 강남3구</option>
            <option value="경기">경기 전체</option>
            <option value="인천">인천</option>
            <option value="기타">기타 지역</option>
          </select>
          <button onclick="applyFilters()" class="bg-brand-600 hover:bg-brand-700 text-white px-5 py-2.5 rounded-xl text-xs font-semibold flex items-center justify-center gap-1 transition shrink-0">
            검색
          </button>
        </div>
      </div>

      <!-- Quick Market Rate Ticker -->
      <div class="mt-6 flex flex-wrap justify-center items-center gap-3 sm:gap-6 text-xs text-slate-400">
        <div class="flex items-center gap-1.5 bg-slate-800/80 px-3 py-1.5 rounded-lg border border-slate-700">
          <span class="text-slate-300 font-medium">C-arm 대진 평균:</span>
          <span class="text-brand-300 font-bold">23 ~ 26만원 / 일</span>
        </div>
        <div class="flex items-center gap-1.5 bg-slate-800/80 px-3 py-1.5 rounded-lg border border-slate-700">
          <span class="text-slate-300 font-medium">일반 X-ray 대진:</span>
          <span class="text-cyan-300 font-bold">18 ~ 22만원 / 일</span>
        </div>
        <div class="flex items-center gap-1.5 bg-slate-800/80 px-3 py-1.5 rounded-lg border border-slate-700">
          <span class="text-slate-300 font-medium">주말/야간 CT 당직:</span>
          <span class="text-emerald-300 font-bold">28 ~ 35만원 / 회</span>
        </div>
      </div>
    </div>
  </section>

  <!-- Main Content Layout -->
  <main class="max-w-6xl mx-auto px-4 py-8 flex-1 w-full">
    
    <!-- Modality Category Selector (장비별 필터) -->
    <div class="mb-6">
      <div class="flex items-center justify-between mb-3">
        <h2 class="text-sm font-bold text-slate-700 flex items-center gap-1.5">
          <i data-lucide="sliders" class="w-4 h-4 text-brand-600"></i>
          <span>보유 장비 및 모달리티 필터</span>
        </h2>
        <span class="text-xs text-slate-400">중복 선택 및 빠른 토글 가능</span>
      </div>

      <div class="flex items-center gap-2 overflow-x-auto pb-2 scrollbar-none" id="modalityChips">
        <button onclick="setModalityFilter('all')" class="modality-chip active px-4 py-2 rounded-xl text-xs font-bold transition flex items-center gap-1.5 shrink-0 bg-brand-700 text-white shadow-sm" data-modality="all">
          <i data-lucide="layers" class="w-3.5 h-3.5"></i>
          <span>전체 장비</span>
        </button>
        <button onclick="setModalityFilter('C-arm')" class="modality-chip px-3.5 py-2 rounded-xl text-xs font-semibold transition flex items-center gap-1.5 shrink-0 bg-white border border-slate-200 text-slate-700 hover:border-brand-500 hover:text-brand-700" data-modality="C-arm">
          <span class="w-2 h-2 rounded-full bg-rose-500"></span>
          <span>C-arm (수술/통증)</span>
        </button>
        <button onclick="setModalityFilter('X-ray')" class="modality-chip px-3.5 py-2 rounded-xl text-xs font-semibold transition flex items-center gap-1.5 shrink-0 bg-white border border-slate-200 text-slate-700 hover:border-brand-500 hover:text-brand-700" data-modality="X-ray">
          <span class="w-2 h-2 rounded-full bg-blue-500"></span>
          <span>일반촬영 (X-ray)</span>
        </button>
        <button onclick="setModalityFilter('CT')" class="modality-chip px-3.5 py-2 rounded-xl text-xs font-semibold transition flex items-center gap-1.5 shrink-0 bg-white border border-slate-200 text-slate-700 hover:border-brand-500 hover:text-brand-700" data-modality="CT">
          <span class="w-2 h-2 rounded-full bg-purple-500"></span>
          <span>CT</span>
        </button>
        <button onclick="setModalityFilter('MRI')" class="modality-chip px-3.5 py-2 rounded-xl text-xs font-semibold transition flex items-center gap-1.5 shrink-0 bg-white border border-slate-200 text-slate-700 hover:border-brand-500 hover:text-brand-700" data-modality="MRI">
          <span class="w-2 h-2 rounded-full bg-indigo-500"></span>
          <span>MRI</span>
        </button>
        <button onclick="setModalityFilter('맘모')" class="modality-chip px-3.5 py-2 rounded-xl text-xs font-semibold transition flex items-center gap-1.5 shrink-0 bg-white border border-slate-200 text-slate-700 hover:border-brand-500 hover:text-brand-700" data-modality="맘모">
          <span class="w-2 h-2 rounded-full bg-pink-500"></span>
          <span>맘모 (유방촬영)</span>
        </button>
        <button onclick="setModalityFilter('초음파')" class="modality-chip px-3.5 py-2 rounded-xl text-xs font-semibold transition flex items-center gap-1.5 shrink-0 bg-white border border-slate-200 text-slate-700 hover:border-brand-500 hover:text-brand-700" data-modality="초음파">
          <span class="w-2 h-2 rounded-full bg-emerald-500"></span>
          <span>초음파 (Sono)</span>
        </button>
        <button onclick="setModalityFilter('BMD')" class="modality-chip px-3.5 py-2 rounded-xl text-xs font-semibold transition flex items-center gap-1.5 shrink-0 bg-white border border-slate-200 text-slate-700 hover:border-brand-500 hover:text-brand-700" data-modality="BMD">
          <span class="w-2 h-2 rounded-full bg-amber-500"></span>
          <span>BMD (골밀도)</span>
        </button>
      </div>
    </div>

    <!-- Sub-Filters: Job Type Tabs & Sorting -->
    <div class="flex flex-col sm:flex-row sm:items-center justify-between gap-3 border-b border-slate-200 pb-3 mb-6">
      <!-- Job Type Tabs -->
      <div class="flex items-center gap-1.5 text-xs font-semibold" id="jobTypeTabs">
        <button onclick="setJobType('all')" class="jobtype-tab px-3 py-1.5 rounded-lg bg-slate-900 text-white transition" data-type="all">전체 공고</button>
        <button onclick="setJobType('urgent')" class="jobtype-tab px-3 py-1.5 rounded-lg text-slate-600 hover:bg-slate-100 transition flex items-center gap-1" data-type="urgent">
          <span class="text-rose-600 font-bold">●</span> 긴급 대진
        </button>
        <button onclick="setJobType('weekend')" class="jobtype-tab px-3 py-1.5 rounded-lg text-slate-600 hover:bg-slate-100 transition" data-type="weekend">주말/야간당직</button>
        <button onclick="setJobType('part')" class="jobtype-tab px-3 py-1.5 rounded-lg text-slate-600 hover:bg-slate-100 transition" data-type="part">정기 파트타임</button>
        <button onclick="setJobType('screening')" class="jobtype-tab px-3 py-1.5 rounded-lg text-slate-600 hover:bg-slate-100 transition" data-type="screening">검진센터</button>
      </div>

      <!-- Result Counter & Sort -->
      <div class="flex items-center justify-between sm:justify-end gap-3 text-xs text-slate-500">
        <div>총 <span id="postCount" class="font-bold text-slate-900">0</span>건</div>
        <div class="flex items-center gap-1">
          <label for="sortBy" class="sr-only">정렬</label>
          <select id="sortBy" onchange="applyFilters()" class="bg-transparent font-medium text-slate-700 focus:outline-none cursor-pointer">
            <option value="latest">최신 등록순</option>
            <option value="payHigh">급여 높은순</option>
            <option value="dateSoon">근무일 임박순</option>
          </select>
        </div>
      </div>
    </div>

    <!-- Job Postings List Grid -->
    <div id="jobList" class="grid grid-cols-1 md:grid-cols-2 gap-4">
      <!-- Dynamic Job Cards will be injected here -->
    </div>

    <!-- Empty State -->
    <div id="emptyState" class="hidden text-center py-16 px-4 bg-white rounded-2xl border border-dashed border-slate-200">
      <div class="w-14 h-14 mx-auto mb-3 rounded-full bg-slate-100 text-slate-400 flex items-center justify-center">
        <i data-lucide="file-question" class="w-7 h-7"></i>
      </div>
      <h3 class="text-base font-bold text-slate-800 mb-1">조건에 맞는 공고가 없습니다</h3>
      <p class="text-xs text-slate-500 mb-4">선택하신 장비, 근무 형태 또는 검색어를 변경해보세요.</p>
      <button onclick="resetFilters()" class="text-xs font-semibold px-4 py-2 rounded-lg bg-brand-50 text-brand-700 hover:bg-brand-100 transition">
        필터 초기화
      </button>
    </div>

  </main>

  <!-- Floating Mobile Post Job Action Button -->
  <div class="fixed bottom-6 right-6 z-30 sm:hidden">
    <button onclick="openPostModal()" class="flex items-center gap-2 bg-slate-900 text-white px-4 py-3 rounded-full shadow-lg shadow-slate-900/40 text-xs font-bold active:scale-95 transition">
      <i data-lucide="plus" class="w-4 h-4 text-brand-400"></i>
      <span>공고 올리기</span>
    </button>
  </div>

  <!-- Footer -->
  <footer class="bg-white border-t border-slate-200 mt-16 py-8 text-xs text-slate-500">
    <div class="max-w-6xl mx-auto px-4 flex flex-col md:flex-row items-center justify-between gap-4">
      <div>
        <div class="flex items-center gap-2 mb-1">
          <span class="font-bold text-slate-800">라드매치 (RadMatch)</span>
          <span class="text-slate-300">|</span>
          <span>방사선사 전문 구인구직 포털</span>
        </div>
        <p class="text-slate-400">본 사이트는 방사선사 면허 소지자의 구인·구직 매칭 편의를 지원하는 중개 플랫폼입니다.</p>
      </div>
      <div class="flex items-center gap-4 text-slate-600">
        <button onclick="openRateInfoModal()" class="hover:text-brand-600 underline">대진 급여 기준표</button>
        <button onclick="openProfileModal()" class="hover:text-brand-600 underline">내 지원 내역</button>
        <button onclick="resetSampleData()" class="text-slate-400 hover:text-rose-600">데이터 초기화</button>
      </div>
    </div>
  </footer>

  <!-- ================= MODALS ================= -->

  <!-- 1. Job Detail & Apply Modal -->
  <div id="jobDetailModal" class="fixed inset-0 z-50 hidden modal-backdrop overflow-y-auto p-4 sm:p-6 flex items-center justify-center">
    <div class="bg-white rounded-2xl max-w-xl w-full p-6 shadow-2xl relative animate-in fade-in zoom-in-95 duration-200">
      <button onclick="closeModal('jobDetailModal')" class="absolute top-5 right-5 text-slate-400 hover:text-slate-600 p-1 rounded-lg">
        <i data-lucide="x" class="w-5 h-5"></i>
      </button>

      <div id="jobDetailContent">
        <!-- Injected via JavaScript -->
      </div>
    </div>
  </div>

  <!-- 2. Fast Apply Confirmation Modal -->
  <div id="applyModal" class="fixed inset-0 z-50 hidden modal-backdrop overflow-y-auto p-4 sm:p-6 flex items-center justify-center">
    <div class="bg-white rounded-2xl max-w-md w-full p-6 shadow-2xl relative">
      <button onclick="closeModal('applyModal')" class="absolute top-5 right-5 text-slate-400 hover:text-slate-600 p-1">
        <i data-lucide="x" class="w-5 h-5"></i>
      </button>

      <div class="flex items-center gap-3 mb-4">
        <div class="w-10 h-10 rounded-xl bg-brand-50 text-brand-700 flex items-center justify-center">
          <i data-lucide="send" class="w-5 h-5"></i>
        </div>
        <div>
          <h3 class="text-base font-bold text-slate-900">간편 대진 지원서 작성</h3>
          <p class="text-xs text-slate-500" id="applyHospitalTitle">병원명</p>
        </div>
      </div>

      <form id="applyForm" onsubmit="submitApplication(event)" class="space-y-3.5 text-xs">
        <input type="hidden" id="applyJobId">

        <div>
          <label class="block font-semibold text-slate-700 mb-1">성명 <span class="text-rose-500">*</span></label>
          <input type="text" id="applicantName" required placeholder="예: 김방사" class="w-full border border-slate-200 rounded-lg p-2.5 text-slate-800 focus:outline-none focus:border-brand-500">
        </div>

        <div class="grid grid-cols-2 gap-2">
          <div>
            <label class="block font-semibold text-slate-700 mb-1">연락처 <span class="text-rose-500">*</span></label>
            <input type="tel" id="applicantPhone" required placeholder="010-1234-5678" class="w-full border border-slate-200 rounded-lg p-2.5 text-slate-800 focus:outline-none focus:border-brand-500">
          </div>
          <div>
            <label class="block font-semibold text-slate-700 mb-1">방사선사 면허 상태</label>
            <select id="applicantLicense" class="w-full border border-slate-200 rounded-lg p-2.5 text-slate-800 focus:outline-none focus:border-brand-500 bg-white">
              <option value="면허보유 (보수교육 이수)">면허보유 (보수교육 완료)</option>
              <option value="면허보유 (신규/이수예정)">면허보유 (신규)</option>
            </select>
          </div>
        </div>

        <div class="grid grid-cols-2 gap-2">
          <div>
            <label class="block font-semibold text-slate-700 mb-1">임상 경력</label>
            <select id="applicantExp" class="w-full border border-slate-200 rounded-lg p-2.5 text-slate-800 focus:outline-none focus:border-brand-500 bg-white">
              <option value="신입 (1년 미만)">신입 (1년 미만)</option>
              <option value="1~3년 차">1~3년 차</option>
              <option value="3~5년 차" selected>3~5년 차</option>
              <option value="5~10년 차">5~10년 차</option>
              <option value="10년 이상 (베테랑)">10년 이상 (베테랑)</option>
            </select>
          </div>
          <div>
            <label class="block font-semibold text-slate-700 mb-1">주요 다룰 수 있는 장비</label>
            <input type="text" id="applicantEquip" placeholder="예: C-arm, 일반촬영" class="w-full border border-slate-200 rounded-lg p-2.5 text-slate-800 focus:outline-none focus:border-brand-500">
          </div>
        </div>

        <div>
          <label class="block font-semibold text-slate-700 mb-1">원장님/담당자 전달 메시지</label>
          <textarea id="applicantMessage" rows="2" placeholder="시간 엄수 및 신속 정확한 촬영 가능합니다. 통장사본 및 면허증 준비되어 있습니다." class="w-full border border-slate-200 rounded-lg p-2.5 text-slate-800 focus:outline-none focus:border-brand-500"></textarea>
        </div>

        <div class="bg-amber-50 border border-amber-200 rounded-lg p-2.5 text-[11px] text-amber-800 leading-tight">
          💡 지원 완료 시 담당자에게 알림이 발송되며, 승인 시 입력하신 연락처로 출근 안내 문자가 발송됩니다.
        </div>

        <div class="flex items-center gap-2 pt-2">
          <button type="button" onclick="closeModal('applyModal')" class="flex-1 py-2.5 rounded-lg border border-slate-200 text-slate-600 font-semibold hover:bg-slate-50 transition">
            취소
          </button>
          <button type="submit" class="flex-1 py-2.5 rounded-lg bg-brand-600 hover:bg-brand-700 text-white font-bold transition shadow-sm">
            대진 지원서 전송
          </button>
        </div>
      </form>
    </div>
  </div>

  <!-- 3. Post New Job Modal (구인 등록) -->
  <div id="postJobModal" class="fixed inset-0 z-50 hidden modal-backdrop overflow-y-auto p-4 sm:p-6 flex items-center justify-center">
    <div class="bg-white rounded-2xl max-w-lg w-full p-6 shadow-2xl relative">
      <button onclick="closeModal('postJobModal')" class="absolute top-5 right-5 text-slate-400 hover:text-slate-600 p-1">
        <i data-lucide="x" class="w-5 h-5"></i>
      </button>

      <div class="flex items-center gap-3 mb-4">
        <div class="w-10 h-10 rounded-xl bg-slate-900 text-brand-400 flex items-center justify-center">
          <i data-lucide="hospital" class="w-5 h-5"></i>
        </div>
        <div>
          <h3 class="text-base font-bold text-slate-900">방사선사 구인 / 대진 공고 등록</h3>
          <p class="text-xs text-slate-500">긴급 대진 및 파트타임 방사선사를 신속하게 매칭해 드립니다.</p>
        </div>
      </div>

      <form id="newJobForm" onsubmit="submitNewJob(event)" class="space-y-3.5 text-xs">
        <div>
          <label class="block font-semibold text-slate-700 mb-1">병원/의원 명칭 <span class="text-rose-500">*</span></label>
          <input type="text" id="postHospital" required placeholder="예: 서울바른정형외과의원" class="w-full border border-slate-200 rounded-lg p-2.5 text-slate-800 focus:outline-none focus:border-brand-500">
        </div>

        <div class="grid grid-cols-2 gap-2">
          <div>
            <label class="block font-semibold text-slate-700 mb-1">지역(권역) <span class="text-rose-500">*</span></label>
            <select id="postRegion" class="w-full border border-slate-200 rounded-lg p-2.5 text-slate-800 focus:outline-none focus:border-brand-500 bg-white">
              <option value="강남/서초/송파">서울 강남/서초/송파</option>
              <option value="서울">서울 기타</option>
              <option value="경기">경기 남부/북부</option>
              <option value="인천">인천</option>
              <option value="기타">기타 지역</option>
            </select>
          </div>
          <div>
            <label class="block font-semibold text-slate-700 mb-1">상세 위치 <span class="text-rose-500">*</span></label>
            <input type="text" id="postLocationDetail" required placeholder="예: 강남역 4번 출구 도보 2분" class="w-full border border-slate-200 rounded-lg p-2.5 text-slate-800 focus:outline-none focus:border-brand-500">
          </div>
        </div>

        <div>
          <label class="block font-semibold text-slate-700 mb-1">모집 공고 제목 <span class="text-rose-500">*</span></label>
          <input type="text" id="postTitle" required placeholder="예: [급구] 이번 주 금요일 C-arm 수술실 1일 대진 구합니다" class="w-full border border-slate-200 rounded-lg p-2.5 text-slate-800 focus:outline-none focus:border-brand-500">
        </div>

        <div class="grid grid-cols-2 gap-2">
          <div>
            <label class="block font-semibold text-slate-700 mb-1">근무 형태 <span class="text-rose-500">*</span></label>
            <select id="postJobType" class="w-full border border-slate-200 rounded-lg p-2.5 text-slate-800 focus:outline-none focus:border-brand-500 bg-white">
              <option value="urgent">긴급 대진 (1~2일)</option>
              <option value="weekend">주말/야간 당직</option>
              <option value="part">정기 파트타임</option>
              <option value="screening">건강검진센터 단기</option>
            </select>
          </div>
          <div>
            <label class="block font-semibold text-slate-700 mb-1">지급 급여 (일급/시급) <span class="text-rose-500">*</span></label>
            <input type="text" id="postPay" required placeholder="예: 일급 250,000원 (당일지급)" class="w-full border border-slate-200 rounded-lg p-2.5 text-slate-800 focus:outline-none focus:border-brand-500">
          </div>
        </div>

        <div>
          <label class="block font-semibold text-slate-700 mb-1">사용 장비 (복수 선택)</label>
          <div class="grid grid-cols-4 gap-2 text-[11px]">
            <label class="flex items-center gap-1.5 p-2 rounded-lg border border-slate-200 cursor-pointer hover:bg-slate-50">
              <input type="checkbox" name="postEquip" value="C-arm" class="rounded text-brand-600 focus:ring-0">
              <span>C-arm</span>
            </label>
            <label class="flex items-center gap-1.5 p-2 rounded-lg border border-slate-200 cursor-pointer hover:bg-slate-50">
              <input type="checkbox" name="postEquip" value="X-ray" checked class="rounded text-brand-600 focus:ring-0">
              <span>X-ray</span>
            </label>
            <label class="flex items-center gap-1.5 p-2 rounded-lg border border-slate-200 cursor-pointer hover:bg-slate-50">
              <input type="checkbox" name="postEquip" value="CT" class="rounded text-brand-600 focus:ring-0">
              <span>CT</span>
            </label>
            <label class="flex items-center gap-1.5 p-2 rounded-lg border border-slate-200 cursor-pointer hover:bg-slate-50">
              <input type="checkbox" name="postEquip" value="MRI" class="rounded text-brand-600 focus:ring-0">
              <span>MRI</span>
            </label>
            <label class="flex items-center gap-1.5 p-2 rounded-lg border border-slate-200 cursor-pointer hover:bg-slate-50">
              <input type="checkbox" name="postEquip" value="맘모" class="rounded text-brand-600 focus:ring-0">
              <span>맘모</span>
            </label>
            <label class="flex items-center gap-1.5 p-2 rounded-lg border border-slate-200 cursor-pointer hover:bg-slate-50">
              <input type="checkbox" name="postEquip" value="초음파" class="rounded text-brand-600 focus:ring-0">
              <span>초음파</span>
            </label>
            <label class="flex items-center gap-1.5 p-2 rounded-lg border border-slate-200 cursor-pointer hover:bg-slate-50">
              <input type="checkbox" name="postEquip" value="BMD" class="rounded text-brand-600 focus:ring-0">
              <span>BMD</span>
            </label>
          </div>
        </div>

        <div class="grid grid-cols-2 gap-2">
          <div>
            <label class="block font-semibold text-slate-700 mb-1">근무 날짜 <span class="text-rose-500">*</span></label>
            <input type="text" id="postWorkDate" required placeholder="예: 2026.10.24(토) 1일" class="w-full border border-slate-200 rounded-lg p-2.5 text-slate-800 focus:outline-none focus:border-brand-500">
          </div>
          <div>
            <label class="block font-semibold text-slate-700 mb-1">근무 시간 <span class="text-rose-500">*</span></label>
            <input type="text" id="postWorkTime" required placeholder="예: 09:00 ~ 18:00 (점심 1시간)" class="w-full border border-slate-200 rounded-lg p-2.5 text-slate-800 focus:outline-none focus:border-brand-500">
          </div>
        </div>

        <div>
          <label class="block font-semibold text-slate-700 mb-1">세부 업무 및 우대사항</label>
          <textarea id="postDescription" rows="2.5" placeholder="예: 정형외과 외래 일반촬영 및 블록 시 C-arm 조작. 환자 건수 일 30건 내외로 여유로운 편입니다. 중식 제공되며 당일 통장으로 입금됩니다." class="w-full border border-slate-200 rounded-lg p-2.5 text-slate-800 focus:outline-none focus:border-brand-500"></textarea>
        </div>

        <div class="grid grid-cols-2 gap-2">
          <div>
            <label class="block font-semibold text-slate-700 mb-1">담당자/원장님 연락처 <span class="text-rose-500">*</span></label>
            <input type="text" id="postContact" required placeholder="예: 010-9876-5432" class="w-full border border-slate-200 rounded-lg p-2.5 text-slate-800 focus:outline-none focus:border-brand-500">
          </div>
          <div>
            <label class="block font-semibold text-slate-700 mb-1">복리후생 / 편의</label>
            <input type="text" id="postPerks" placeholder="예: 중식제공, 3.3%공제, 당일지급" class="w-full border border-slate-200 rounded-lg p-2.5 text-slate-800 focus:outline-none focus:border-brand-500">
          </div>
        </div>

        <div class="flex items-center gap-2 pt-2">
          <button type="button" onclick="closeModal('postJobModal')" class="flex-1 py-2.5 rounded-lg border border-slate-200 text-slate-600 font-semibold hover:bg-slate-50 transition">
            취소
          </button>
          <button type="submit" class="flex-1 py-2.5 rounded-lg bg-slate-900 hover:bg-slate-800 text-brand-300 font-bold transition shadow-sm">
            공고 즉시 등록하기
          </button>
        </div>
      </form>
    </div>
  </div>

  <!-- 4. Profile & Applied Jobs Modal -->
  <div id="profileModal" class="fixed inset-0 z-50 hidden modal-backdrop overflow-y-auto p-4 sm:p-6 flex items-center justify-center">
    <div class="bg-white rounded-2xl max-w-xl w-full p-6 shadow-2xl relative">
      <button onclick="closeModal('profileModal')" class="absolute top-5 right-5 text-slate-400 hover:text-slate-600 p-1">
        <i data-lucide="x" class="w-5 h-5"></i>
      </button>

      <div class="flex items-center gap-3 mb-6">
        <div class="w-12 h-12 rounded-2xl bg-brand-500/10 text-brand-700 flex items-center justify-center font-bold text-xl">
          <i data-lucide="badge-check" class="w-6 h-6"></i>
        </div>
        <div>
          <h3 class="text-lg font-bold text-slate-900">내 방사선사 프로필 & 지원 현황</h3>
          <p class="text-xs text-slate-500">지원한 공고 상태와 저장된 프로필을 관리합니다.</p>
        </div>
      </div>

      <!-- Tabs: My Applications vs My Profile Settings -->
      <div class="flex border-b border-slate-200 mb-4 text-xs font-bold">
        <button onclick="switchProfileTab('apps')" id="tabBtnApps" class="pb-2.5 px-3 border-b-2 border-brand-600 text-brand-700 transition">
          지원 완료 목록 (<span id="myAppsCount">0</span>)
        </button>
        <button onclick="switchProfileTab('info')" id="tabBtnInfo" class="pb-2.5 px-3 border-b-2 border-transparent text-slate-500 hover:text-slate-800 transition">
          내 기본 프로필 설정
        </button>
      </div>

      <!-- Tab Content: Applications -->
      <div id="profileAppsContent" class="space-y-3 max-h-80 overflow-y-auto pr-1">
        <!-- Dynamically injected -->
      </div>

      <!-- Tab Content: Profile Settings -->
      <div id="profileInfoContent" class="hidden space-y-3 text-xs">
        <div>
          <label class="block font-semibold text-slate-700 mb-1">기본 이름</label>
          <input type="text" id="prefName" class="w-full border border-slate-200 rounded-lg p-2.5" placeholder="예: 김방사">
        </div>
        <div>
          <label class="block font-semibold text-slate-700 mb-1">기본 연락처</label>
          <input type="tel" id="prefPhone" class="w-full border border-slate-200 rounded-lg p-2.5" placeholder="예: 010-0000-0000">
        </div>
        <div class="grid grid-cols-2 gap-2">
          <div>
            <label class="block font-semibold text-slate-700 mb-1">기본 경력</label>
            <select id="prefExp" class="w-full border border-slate-200 rounded-lg p-2.5 bg-white">
              <option value="1~3년 차">1~3년 차</option>
              <option value="3~5년 차" selected>3~5년 차</option>
              <option value="5~10년 차">5~10년 차</option>
              <option value="10년 이상">10년 이상</option>
            </select>
          </div>
          <div>
            <label class="block font-semibold text-slate-700 mb-1">주력 장비</label>
            <input type="text" id="prefEquip" class="w-full border border-slate-200 rounded-lg p-2.5" placeholder="C-arm, 일반촬영, CT">
          </div>
        </div>
        <div>
          <label class="block font-semibold text-slate-700 mb-1">자주 쓰는 지원 각오</label>
          <textarea id="prefBio" rows="2" class="w-full border border-slate-200 rounded-lg p-2.5" placeholder="대진 경력 다수 있으며 환자 케어 및 원내 장비 숙련도가 높습니다."></textarea>
        </div>
        <button onclick="saveUserProfile()" class="w-full py-2.5 rounded-lg bg-brand-600 hover:bg-brand-700 text-white font-bold transition">
          프로필 정보 저장하기
        </button>
      </div>

    </div>
  </div>

  <!-- 5. Market Rate Guide Modal -->
  <div id="rateInfoModal" class="fixed inset-0 z-50 hidden modal-backdrop overflow-y-auto p-4 sm:p-6 flex items-center justify-center">
    <div class="bg-white rounded-2xl max-w-lg w-full p-6 shadow-2xl relative">
      <button onclick="closeModal('rateInfoModal')" class="absolute top-5 right-5 text-slate-400 hover:text-slate-600 p-1">
        <i data-lucide="x" class="w-5 h-5"></i>
      </button>

      <div class="flex items-center gap-3 mb-4">
        <div class="w-10 h-10 rounded-xl bg-emerald-50 text-emerald-700 flex items-center justify-center font-bold">
          <i data-lucide="calculator" class="w-5 h-5"></i>
        </div>
        <div>
          <h3 class="text-base font-bold text-slate-900">방사선사 대진·알바 적정 시세 가이드</h3>
          <p class="text-xs text-slate-500">수도권 및 주요 지역 실제 체결 기준 평균 시세표</p>
        </div>
      </div>

      <div class="space-y-3 text-xs">
        <div class="p-3 rounded-xl bg-slate-50 border border-slate-100 flex items-center justify-between">
          <div>
            <div class="font-bold text-slate-800">C-arm 대진 (정형외과/신경외과/통증)</div>
            <div class="text-[11px] text-slate-500">09:00 ~ 18:00 (8시간 기준)</div>
          </div>
          <div class="text-right">
            <span class="font-extrabold text-brand-700 text-sm">230,000 ~ 270,000원</span>
            <div class="text-[10px] text-emerald-600 font-semibold">당일 지급 다수</div>
          </div>
        </div>

        <div class="p-3 rounded-xl bg-slate-50 border border-slate-100 flex items-center justify-between">
          <div>
            <div class="font-bold text-slate-800">일반촬영(X-ray) 대진 (외래의원)</div>
            <div class="text-[11px] text-slate-500">09:00 ~ 18:00 (8시간 기준)</div>
          </div>
          <div class="text-right">
            <span class="font-extrabold text-brand-700 text-sm">180,000 ~ 220,000원</span>
            <div class="text-[10px] text-slate-500">중식 포함 여부 확인</div>
          </div>
        </div>

        <div class="p-3 rounded-xl bg-slate-50 border border-slate-100 flex items-center justify-between">
          <div>
            <div class="font-bold text-slate-800">종합병원 응급실 CT/X-ray 야간당직</div>
            <div class="text-[11px] text-slate-500">20:00 ~ 익일 08:00 (12시간 기준)</div>
          </div>
          <div class="text-right">
            <span class="font-extrabold text-brand-700 text-sm">280,000 ~ 350,000원</span>
            <div class="text-[10px] text-purple-600 font-semibold">당직실/식사 제공</div>
          </div>
        </div>

        <div class="p-3 rounded-xl bg-slate-50 border border-slate-100 flex items-center justify-between">
          <div>
            <div class="font-bold text-slate-800">건강검진 맘모(Mammography) 오전 알바</div>
            <div class="text-[11px] text-slate-500">07:30 ~ 12:30 (5시간 단기)</div>
          </div>
          <div class="text-right">
            <span class="font-extrabold text-brand-700 text-sm">시급 26,000 ~ 30,000원</span>
            <div class="text-[10px] text-pink-600 font-semibold">여성 방사선사 우대</div>
          </div>
        </div>
      </div>

      <div class="mt-4 p-3 rounded-xl bg-slate-100 text-[11px] text-slate-600 leading-normal">
        📌 <strong>참고사항:</strong> 3.3% 사업소득세 공제 여부 및 식대 제공, 교통비 지원 여부에 따라 실제 수령액이 달라질 수 있습니다. 출근 전 반드시 구인처와 상세 조건을 확인하세요.
      </div>
    </div>
  </div>

  <!-- Toast Notification Container -->
  <div id="toastContainer" class="fixed bottom-5 left-1/2 -translate-x-1/2 z-50 flex flex-col gap-2 pointer-events-none"></div>

  <!-- Application Logic JavaScript -->
  <script>
    // Initial Seed Data for Radiological Technologist Part-time Jobs
    const SEED_JOBS = [
      {
        id: 'job-1',
        hospital: '강남바른정형외과의원',
        regionGroup: '강남/서초/송파',
        location: '서울 강남구 테헤란로 152 (역삼역 3번출구 도보 1분)',
        title: '[급구/당일지급] 이번 주 금요일 정형외과 C-arm 및 일반촬영 1일 대진 구합니다',
        type: 'urgent',
        typeName: '긴급대진',
        pay: '일급 260,000원',
        payAmount: 260000,
        payType: '일급',
        workDate: '2026.10.23(금) 1일간',
        workTime: '09:00 ~ 18:00 (점심시간 13:00~14:00)',
        equipment: ['C-arm', 'X-ray'],
        perks: ['중식 제공', '당일 즉시 송금', '3.3% 원천징수'],
        desc: '원장님 수술 일정으로 외래 일반촬영 및 블록 시 C-arm 조작해주실 선생님 모십니다. C-arm 조작 익숙하신 분 환영하며, 장비는 지멘스 장비입니다. 직원 휴게실 완비되어 있으며 분위기 매우 편안합니다.',
        contact: '010-4821-3920 (총괄실장)',
        postedAt: '10분 전',
        timestamp: Date.now() - 1000 * 60 * 10
      },
      {
        id: 'job-2',
        hospital: '연세마디튼튼병원',
        regionGroup: '경기',
        location: '경기 성남시 분당구 야탑로 64 (야탑역 2번출구)',
        title: '[주말당직] 토/일 종합병원 응급실 CT 및 포터블 야간 당직 선생님 모십니다',
        type: 'weekend',
        typeName: '주말당직',
        pay: '일급 340,000원',
        payAmount: 340000,
        payType: '일급',
        workDate: '2026.10.24(토) 18:00 ~ 10.25(일) 09:00',
        workTime: '18:00 ~ 익일 09:00 (야간 15시간)',
        equipment: ['CT', 'X-ray'],
        perks: ['개인 당직실 제공', '야식비 지원', '당일 지급'],
        desc: '응급실 내원 환자 뇌/복부 CT 및 일반촬영 전담 당직입니다. CT는 GE 128채널 사용 중이며 프로토콜 정리 잘 되어 있습니다. 야간에 응급환자 없을 시 당직실에서 편히 휴식 가능합니다.',
        contact: '010-9281-7712 (영상의학팀장)',
        postedAt: '35분 전',
        timestamp: Date.now() - 1000 * 60 * 35
      },
      {
        id: 'job-3',
        hospital: '미래메디컬 건강증진센터',
        regionGroup: '서울',
        location: '서울 영등포구 여의대로 108 (여의도역)',
        title: '[오전단기] 평일 오전 검진 맘모(유방촬영) & BMD 알바 (시즌 단기 2주)',
        type: 'screening',
        typeName: '검진단기',
        pay: '시급 29,000원 (일 145,000원)',
        payAmount: 145000,
        payType: '시급',
        workDate: '다음 주 월~금 (2주간 협의)',
        workTime: '07:30 ~ 12:30 (오전 5시간)',
        equipment: ['맘모', 'BMD'],
        perks: ['주차 무료', '간식 제공', '여성 방사선사'],
        desc: '하반기 검진 성수기로 오전 맘모 및 골밀도 검사 전담해주실 방사선사님 구합니다. 홀로직 디지털 맘모 사용 중이며 포지셔닝 능숙하신 경력자 선생님 우대합니다.',
        contact: '010-3321-4490 (검진센터 행정실)',
        postedAt: '1시간 전',
        timestamp: Date.now() - 1000 * 60 * 65
      },
      {
        id: 'job-4',
        hospital: '송파서울신경외과의원',
        regionGroup: '강남/서초/송파',
        location: '서울 송파구 올림픽로 300 (잠실역 8번출구)',
        title: '[단기대진] 화요일 C-arm 척추 신경차단술 1일 대진 구합니다 (건수 여유)',
        type: 'urgent',
        typeName: '긴급대진',
        pay: '일급 250,000원',
        payAmount: 250000,
        payType: '일급',
        workDate: '2026.10.27(화) 09:00 ~ 18:00',
        workTime: '09:00 ~ 18:00 (중식 13:00~14:00)',
        equipment: ['C-arm'],
        perks: ['중식 제공', '오버타임 없음', '당일입금'],
        desc: '기존 근무자 예비군 훈련으로 1일 C-arm 대진 모십니다. 척추 신경차단술 위주이며 하루 15~20건 내외입니다. 정시 퇴근 칼같이 지켜드립니다.',
        contact: '010-5544-1239 (원무과장)',
        postedAt: '2시간 전',
        timestamp: Date.now() - 1000 * 60 * 120
      },
      {
        id: 'job-5',
        hospital: '웰빙영상의학과의원',
        regionGroup: '서울',
        location: '서울 마포구 양화로 160 (홍대입구역 9번출구)',
        title: '[파트타임] 오후 MRI(1.5T / 3.0T) 검사 전담 파트타임 방사선사 채용',
        type: 'part',
        typeName: '정기파트',
        pay: '시급 32,000원',
        payAmount: 160000,
        payType: '시급',
        workDate: '매주 화, 목, 토 (요일 협의 가능)',
        workTime: '14:00 ~ 19:00 (5시간)',
        equipment: ['MRI'],
        perks: ['주휴수당 별도', '4대보험 가입 가능', '유니폼 지급'],
        desc: '정형외과 관절 및 척추 MRI 스캔 전담 파트타임입니다. 필립스 3.0T 인제니아 보유 중이며 스캔 프로토콜 잘 세팅되어 있습니다. 경력자분 많은 지원 바랍니다.',
        contact: '010-8812-9900 (대표원장)',
        postedAt: '3시간 전',
        timestamp: Date.now() - 1000 * 60 * 180
      },
      {
        id: 'job-6',
        hospital: '수원센트럴정형외과',
        regionGroup: '경기',
        location: '경기 수원시 팔달구 매산로 22 (수원역 로데오)',
        title: '[급구대진] 정형외과 외래 일반촬영 1일 대진 (포터블 없음, 단독)',
        type: 'urgent',
        typeName: '긴급대진',
        pay: '일급 220,000원',
        payAmount: 220000,
        payType: '일급',
        workDate: '2026.10.23(금) 09:00 ~ 18:30',
        workTime: '09:00 ~ 18:30 (토요일 휴진)',
        equipment: ['X-ray'],
        perks: ['점심식사 제공', '칼퇴보장', '당일지급'],
        desc: '외래 단순 엑스레이 촬영만 해주시면 됩니다. C-arm 수술실 없으며 외래 엑스레이실 단독 근무입니다. 리스트오더 및 PACS 연동 원활합니다.',
        contact: '010-3311-2099 (인사담당)',
        postedAt: '5시간 전',
        timestamp: Date.now() - 1000 * 60 * 300
      },
      {
        id: 'job-7',
        hospital: '부평바른이비인후과·내과',
        regionGroup: '인천',
        location: '인천 부평구 부평대로 24 (부평역 지하상가 7번)',
        title: '[주말오전] 일요일 오전 흉부X-ray 및 복부초음파 검사 보조 알바',
        type: 'weekend',
        typeName: '주말알바',
        pay: '일급 140,000원',
        payAmount: 140000,
        payType: '일급',
        workDate: '2026.10.25(일) 09:00 ~ 13:00 (4시간)',
        workTime: '09:00 ~ 13:00 (오전 반일)',
        equipment: ['X-ray', '초음파'],
        perks: ['반일 근무', '교통비 지원', '당일 현금/송금'],
        desc: '일요일 오전 진료 중 내과 흉부 엑스레이 및 이비인후과 부비동 X-ray 촬영입니다. 업무 강도 낮고 반일만 일하고 가시면 됩니다.',
        contact: '010-7765-4321 (실장)',
        postedAt: '6시간 전',
        timestamp: Date.now() - 1000 * 60 * 360
      }
    ];

    // App State
    let jobs = [];
    let currentModality = 'all';
    let currentJobType = 'all';
    let currentRegion = 'all';
    let searchQuery = '';
    let currentSort = 'latest';
    let appliedJobs = [];
    let userProfile = {
      name: '',
      phone: '',
      license: '면허보유 (보수교육 이수)',
      exp: '3~5년 차',
      equip: 'C-arm, X-ray',
      bio: '시간 엄수 및 신속 정확한 촬영 가능합니다.'
    };

    // Initialize
    document.addEventListener('DOMContentLoaded', () => {
      loadStorageData();
      renderJobList();
      updateBadges();
      lucide.createIcons();
    });

    // Load from LocalStorage
    function loadStorageData() {
      const storedJobs = localStorage.getItem('radmatch_jobs');
      if (storedJobs) {
        try {
          jobs = JSON.parse(storedJobs);
        } catch (e) {
          jobs = [...SEED_JOBS];
        }
      } else {
        jobs = [...SEED_JOBS];
        saveJobsToStorage();
      }

      const storedApps = localStorage.getItem('radmatch_apps');
      if (storedApps) {
        try {
          appliedJobs = JSON.parse(storedApps);
        } catch (e) {
          appliedJobs = [];
        }
      }

      const storedProfile = localStorage.getItem('radmatch_profile');
      if (storedProfile) {
        try {
          userProfile = JSON.parse(storedProfile);
          populateProfileFields();
        } catch (e) {}
      }
    }

    function saveJobsToStorage() {
      localStorage.setItem('radmatch_jobs', JSON.stringify(jobs));
    }

    function saveAppsToStorage() {
      localStorage.setItem('radmatch_apps', JSON.stringify(appliedJobs));
    }

    function populateProfileFields() {
      if (document.getElementById('prefName')) document.getElementById('prefName').value = userProfile.name || '';
      if (document.getElementById('prefPhone')) document.getElementById('prefPhone').value = userProfile.phone || '';
      if (document.getElementById('prefExp')) document.getElementById('prefExp').value = userProfile.exp || '3~5년 차';
      if (document.getElementById('prefEquip')) document.getElementById('prefEquip').value = userProfile.equip || '';
      if (document.getElementById('prefBio')) document.getElementById('prefBio').value = userProfile.bio || '';

      // Also prefill applicant modal if empty
      if (document.getElementById('applicantName')) document.getElementById('applicantName').value = userProfile.name || '';
      if (document.getElementById('applicantPhone')) document.getElementById('applicantPhone').value = userProfile.phone || '';
      if (document.getElementById('applicantExp')) document.getElementById('applicantExp').value = userProfile.exp || '3~5년 차';
      if (document.getElementById('applicantEquip')) document.getElementById('applicantEquip').value = userProfile.equip || '';
    }

    // Filter Handlers
    function setModalityFilter(modality) {
      currentModality = modality;
      
      // Update UI active states
      document.querySelectorAll('.modality-chip').forEach(btn => {
        if (btn.dataset.modality === modality) {
          btn.className = 'modality-chip active px-4 py-2 rounded-xl text-xs font-bold transition flex items-center gap-1.5 shrink-0 bg-brand-700 text-white shadow-sm';
        } else {
          btn.className = 'modality-chip px-3.5 py-2 rounded-xl text-xs font-semibold transition flex items-center gap-1.5 shrink-0 bg-white border border-slate-200 text-slate-700 hover:border-brand-500 hover:text-brand-700';
        }
      });

      renderJobList();
    }

    function setJobType(type) {
      currentJobType = type;
      
      document.querySelectorAll('.jobtype-tab').forEach(btn => {
        if (btn.dataset.type === type) {
          btn.className = 'jobtype-tab px-3 py-1.5 rounded-lg bg-slate-900 text-white transition font-bold';
        } else {
          btn.className = 'jobtype-tab px-3 py-1.5 rounded-lg text-slate-600 hover:bg-slate-100 transition';
        }
      });

      renderJobList();
    }

    function handleSearch() {
      searchQuery = document.getElementById('searchInput').value.trim().toLowerCase();
      renderJobList();
    }

    function applyFilters() {
      currentRegion = document.getElementById('regionFilter').value;
      currentSort = document.getElementById('sortBy').value;
      renderJobList();
    }

    function resetFilters() {
      currentModality = 'all';
      currentJobType = 'all';
      currentRegion = 'all';
      searchQuery = '';
      document.getElementById('searchInput').value = '';
      document.getElementById('regionFilter').value = 'all';
      document.getElementById('sortBy').value = 'latest';
      
      setModalityFilter('all');
      setJobType('all');
      renderJobList();
    }

    // Render Job Cards
    function renderJobList() {
      const listEl = document.getElementById('jobList');
      const emptyEl = document.getElementById('emptyState');
      const countEl = document.getElementById('postCount');

      // Filter
      let filtered = jobs.filter(job => {
        // Modality match
        if (currentModality !== 'all') {
          if (!job.equipment.includes(currentModality)) return false;
        }

        // Job type match
        if (currentJobType !== 'all') {
          if (job.type !== currentJobType) return false;
        }

        // Region match
        if (currentRegion !== 'all') {
          if (currentRegion === '강남/서초/송파' && job.regionGroup !== '강남/서초/송파') return false;
          if (currentRegion === '서울' && !job.location.includes('서울')) return false;
          if (currentRegion === '경기' && !job.location.includes('경기')) return false;
          if (currentRegion === '인천' && !job.location.includes('인천')) return false;
          if (currentRegion === '기타' && (job.location.includes('서울') || job.location.includes('경기') || job.location.includes('인천'))) return false;
        }

        // Search text match
        if (searchQuery) {
          const content = (job.title + ' ' + job.hospital + ' ' + job.location + ' ' + job.equipment.join(' ') + ' ' + (job.desc || '')).toLowerCase();
          if (!content.includes(searchQuery)) return false;
        }

        return true;
      });

      // Sort
      if (currentSort === 'payHigh') {
        filtered.sort((a, b) => (b.payAmount || 0) - (a.payAmount || 0));
      } else if (currentSort === 'latest') {
        filtered.sort((a, b) => b.timestamp - a.timestamp);
      }

      countEl.innerText = filtered.length;

      if (filtered.length === 0) {
        listEl.innerHTML = '';
        emptyEl.classList.remove('hidden');
        return;
      }

      emptyEl.classList.add('hidden');

      // Render cards
      listEl.innerHTML = filtered.map(job => {
        const isApplied = appliedJobs.some(a => a.jobId === job.id);
        
        // Modality badges markup
        const equipBadges = job.equipment.map(eq => {
          let colorClass = 'bg-slate-100 text-slate-700';
          if (eq === 'C-arm') colorClass = 'bg-rose-50 text-rose-700 border border-rose-200';
          if (eq === 'X-ray') colorClass = 'bg-blue-50 text-blue-700 border border-blue-200';
          if (eq === 'CT') colorClass = 'bg-purple-50 text-purple-700 border border-purple-200';
          if (eq === 'MRI') colorClass = 'bg-indigo-50 text-indigo-700 border border-indigo-200';
          if (eq === '맘모') colorClass = 'bg-pink-50 text-pink-700 border border-pink-200';
          if (eq === '초음파') colorClass = 'bg-emerald-50 text-emerald-700 border border-emerald-200';
          return `<span class="px-2 py-0.5 rounded text-[11px] font-bold ${colorClass}">${eq}</span>`;
        }).join(' ');

        // Type badge markup
        let typeBadge = '';
        if (job.type === 'urgent') {
          typeBadge = '<span class="px-2 py-0.5 rounded bg-rose-500 text-white text-[10px] font-extrabold animate-pulse">급구 대진</span>';
        } else if (job.type === 'weekend') {
          typeBadge = '<span class="px-2 py-0.5 rounded bg-slate-800 text-brand-300 text-[10px] font-bold">주말/야간</span>';
        } else if (job.type === 'screening') {
          typeBadge = '<span class="px-2 py-0.5 rounded bg-amber-500 text-white text-[10px] font-bold">검진 알바</span>';
        } else {
          typeBadge = '<span class="px-2 py-0.5 rounded bg-slate-200 text-slate-700 text-[10px] font-bold">파트타임</span>';
        }

        return `
          <div class="bg-white rounded-2xl p-5 border border-slate-200 shadow-sm hover:shadow-md hover:border-brand-300 transition flex flex-col justify-between group">
            <div>
              <!-- Card Header -->
              <div class="flex items-center justify-between mb-2">
                <div class="flex items-center gap-1.5 flex-wrap">
                  ${typeBadge}
                  <span class="text-xs font-bold text-slate-600">${job.hospital}</span>
                </div>
                <span class="text-[11px] text-slate-400 font-medium">${job.postedAt || '방금 전'}</span>
              </div>

              <!-- Title -->
              <h3 onclick="openJobDetail('${job.id}')" class="text-sm sm:text-base font-bold text-slate-900 group-hover:text-brand-700 transition cursor-pointer mb-2.5 line-clamp-2">
                ${job.title}
              </h3>

              <!-- Modality Chips -->
              <div class="flex flex-wrap gap-1.5 mb-3.5">
                ${equipBadges}
              </div>

              <!-- Work Conditions Grid -->
              <div class="space-y-1.5 text-xs text-slate-600 bg-slate-50 p-3 rounded-xl mb-3.5">
                <div class="flex items-center gap-2">
                  <i data-lucide="calendar" class="w-3.5 h-3.5 text-slate-400 shrink-0"></i>
                  <span class="font-medium text-slate-800 truncate">${job.workDate}</span>
                </div>
                <div class="flex items-center gap-2">
                  <i data-lucide="clock" class="w-3.5 h-3.5 text-slate-400 shrink-0"></i>
                  <span class="text-slate-600 truncate">${job.workTime}</span>
                </div>
                <div class="flex items-center gap-2">
                  <i data-lucide="map-pin" class="w-3.5 h-3.5 text-slate-400 shrink-0"></i>
                  <span class="text-slate-600 truncate">${job.location}</span>
                </div>
              </div>
            </div>

            <!-- Card Bottom: Pay & Apply CTA -->
            <div class="pt-3 border-t border-slate-100 flex items-center justify-between gap-3">
              <div>
                <span class="text-[10px] text-slate-400 block font-medium">지급 급여</span>
                <span class="text-base sm:text-lg font-black text-slate-900 text-brand-700">${job.pay}</span>
              </div>

              <div class="flex items-center gap-1.5">
                <button onclick="openJobDetail('${job.id}')" class="text-xs font-semibold px-3 py-2 rounded-xl text-slate-600 bg-slate-100 hover:bg-slate-200 transition">
                  상세보기
                </button>
                ${isApplied ? `
                  <button disabled class="text-xs font-bold px-3.5 py-2 rounded-xl bg-slate-200 text-slate-500 cursor-not-allowed flex items-center gap-1">
                    <i data-lucide="check" class="w-3.5 h-3.5"></i>
                    지원완료
                  </button>
                ` : `
                  <button onclick="openApplyModal('${job.id}')" class="text-xs font-bold px-3.5 py-2 rounded-xl bg-brand-600 hover:bg-brand-700 text-white shadow-sm shadow-brand-500/20 transition flex items-center gap-1">
                    대진 지원
                  </button>
                `}
              </div>
            </div>
          </div>
        `;
      }).join('');

      lucide.createIcons();
    }

    // Modal Handlers
    function openModal(id) {
      const modal = document.getElementById(id);
      if (modal) {
        modal.classList.remove('hidden');
        lucide.createIcons();
      }
    }

    function closeModal(id) {
      const modal = document.getElementById(id);
      if (modal) {
        modal.classList.add('hidden');
      }
    }

    // Job Detail View
    function openJobDetail(jobId) {
      const job = jobs.find(j => j.id === jobId);
      if (!job) return;

      const isApplied = appliedJobs.some(a => a.jobId === job.id);
      const detailContainer = document.getElementById('jobDetailContent');

      detailContainer.innerHTML = `
        <div class="flex items-center gap-2 mb-2">
          <span class="px-2 py-0.5 rounded bg-brand-50 text-brand-700 text-[11px] font-bold border border-brand-200">${job.typeName || '대진'}</span>
          <span class="text-xs font-bold text-slate-500">${job.hospital}</span>
        </div>

        <h2 class="text-lg sm:text-xl font-black text-slate-900 mb-3 leading-snug">${job.title}</h2>

        <div class="bg-brand-50/60 border border-brand-100 rounded-2xl p-4 mb-4 flex items-center justify-between">
          <div>
            <span class="text-xs text-brand-800 font-semibold block">약정 급여</span>
            <span class="text-xl sm:text-2xl font-black text-brand-900">${job.pay}</span>
          </div>
          <div class="text-right">
            <span class="text-[11px] text-slate-500 block">정산 방식</span>
            <span class="text-xs font-bold text-slate-800">${job.perks?.includes('당일 즉시 송금') || job.perks?.includes('당일지급') ? '당일 근무 후 즉시 송금' : '월말 정산 / 협의'}</span>
          </div>
        </div>

        <div class="space-y-3 text-xs mb-6">
          <div class="p-3 bg-slate-50 rounded-xl space-y-2">
            <div class="flex items-start gap-2">
              <span class="font-bold text-slate-700 w-20 shrink-0">근무 일자:</span>
              <span class="text-slate-900 font-semibold">${job.workDate}</span>
            </div>
            <div class="flex items-start gap-2">
              <span class="font-bold text-slate-700 w-20 shrink-0">근무 시간:</span>
              <span class="text-slate-900">${job.workTime}</span>
            </div>
            <div class="flex items-start gap-2">
              <span class="font-bold text-slate-700 w-20 shrink-0">병원 위치:</span>
              <span class="text-slate-900">${job.location}</span>
            </div>
            <div class="flex items-start gap-2">
              <span class="font-bold text-slate-700 w-20 shrink-0">촬영 장비:</span>
              <div class="flex flex-wrap gap-1">
                ${job.equipment.map(e => `<span class="bg-white border border-slate-200 px-2 py-0.5 rounded font-bold text-brand-700">${e}</span>`).join('')}
              </div>
            </div>
          </div>

          <div>
            <h4 class="font-bold text-slate-800 mb-1.5 flex items-center gap-1.5">
              <i data-lucide="file-text" class="w-3.5 h-3.5 text-brand-600"></i>
              <span>상세 업무 내용 및 특이사항</span>
            </h4>
            <p class="text-slate-600 leading-relaxed bg-slate-50 p-3.5 rounded-xl border border-slate-100 whitespace-pre-line text-xs">
              ${job.desc || '별도 세부 기재사항이 없습니다.'}
            </p>
          </div>

          <div>
            <h4 class="font-bold text-slate-800 mb-1 flex items-center gap-1.5">
              <i data-lucide="gift" class="w-3.5 h-3.5 text-brand-600"></i>
              <span>근무 혜택 및 편의</span>
            </h4>
            <div class="flex flex-wrap gap-1.5">
              ${(job.perks || ['중식 지원', '당일 정산']).map(p => `<span class="bg-slate-100 text-slate-700 px-2.5 py-1 rounded-lg text-[11px] font-medium">✓ ${p}</span>`).join('')}
            </div>
          </div>

          <div class="bg-slate-100 p-3 rounded-xl flex items-center justify-between text-xs">
            <span class="font-bold text-slate-700">채용 문의처</span>
            <span class="font-mono font-bold text-slate-900">${job.contact}</span>
          </div>
        </div>

        <div class="flex items-center gap-2 pt-2 border-t border-slate-100">
          <button onclick="closeModal('jobDetailModal')" class="flex-1 py-3 rounded-xl border border-slate-200 text-slate-600 font-semibold text-xs hover:bg-slate-50 transition">
            닫기
          </button>
          ${isApplied ? `
            <button disabled class="flex-1 py-3 rounded-xl bg-slate-200 text-slate-500 font-bold text-xs cursor-not-allowed">
              이미 지원 완료된 공고입니다
            </button>
          ` : `
            <button onclick="openApplyModal('${job.id}'); closeModal('jobDetailModal');" class="flex-1 py-3 rounded-xl bg-brand-600 hover:bg-brand-700 text-white font-bold text-xs shadow-md transition">
              대진 지원하기
            </button>
          `}
        </div>
      `;

      openModal('jobDetailModal');
    }

    // Apply Modal
    function openApplyModal(jobId) {
      const job = jobs.find(j => j.id === jobId);
      if (!job) return;

      document.getElementById('applyJobId').value = job.id;
      document.getElementById('applyHospitalTitle').innerText = `${job.hospital} - ${job.title}`;

      // Populate user info if exists
      if (userProfile.name) document.getElementById('applicantName').value = userProfile.name;
      if (userProfile.phone) document.getElementById('applicantPhone').value = userProfile.phone;
      if (userProfile.equip) document.getElementById('applicantEquip').value = userProfile.equip;
      if (userProfile.bio) document.getElementById('applicantMessage').value = userProfile.bio;

      openModal('applyModal');
    }

    function submitApplication(event) {
      event.preventDefault();
      const jobId = document.getElementById('applyJobId').value;
      const job = jobs.find(j => j.id === jobId);
      if (!job) return;

      const applicant = {
        jobId: job.id,
        hospital: job.hospital,
        title: job.title,
        workDate: job.workDate,
        pay: job.pay,
        name: document.getElementById('applicantName').value.trim(),
        phone: document.getElementById('applicantPhone').value.trim(),
        license: document.getElementById('applicantLicense').value,
        exp: document.getElementById('applicantExp').value,
        equip: document.getElementById('applicantEquip').value.trim(),
        message: document.getElementById('applicantMessage').value.trim(),
        appliedAt: new Date().toLocaleDateString('ko-KR') + ' ' + new Date().toLocaleTimeString('ko-KR', {hour: '2-digit', minute:'2-digit'}),
        status: '지원서 접수 완료'
      };

      // Auto update profile cache
      userProfile.name = applicant.name;
      userProfile.phone = applicant.phone;
      userProfile.exp = applicant.exp;
      userProfile.equip = applicant.equip;
      localStorage.setItem('radmatch_profile', JSON.stringify(userProfile));

      appliedJobs.unshift(applicant);
      saveAppsToStorage();

      closeModal('applyModal');
      renderJobList();
      updateBadges();

      showToast(`🎉 ${job.hospital} 대진 지원이 성공적으로 전송되었습니다!`, 'success');
    }

    // Post Job Modal
    function openPostModal() {
      openModal('postJobModal');
    }

    function submitNewJob(event) {
      event.preventDefault();

      const hospital = document.getElementById('postHospital').value.trim();
      const regionGroup = document.getElementById('postRegion').value;
      const location = document.getElementById('postLocationDetail').value.trim();
      const title = document.getElementById('postTitle').value.trim();
      const type = document.getElementById('postJobType').value;
      const pay = document.getElementById('postPay').value.trim();
      const workDate = document.getElementById('postWorkDate').value.trim();
      const workTime = document.getElementById('postWorkTime').value.trim();
      const desc = document.getElementById('postDescription').value.trim();
      const contact = document.getElementById('postContact').value.trim();
      const perksInput = document.getElementById('postPerks').value.trim();

      // Selected modalities
      const equipNodes = document.querySelectorAll('input[name="postEquip"]:checked');
      const equipment = Array.from(equipNodes).map(n => n.value);
      if (equipment.length === 0) equipment.push('일반촬영(X-ray)');

      // Extract pay number for sorting
      const payNumMatch = pay.replace(/[^0-9]/g, '');
      const payAmount = payNumMatch ? parseInt(payNumMatch, 10) : 200000;

      let typeName = '긴급대진';
      if (type === 'weekend') typeName = '주말/야간당직';
      if (type === 'part') typeName = '정기파트';
      if (type === 'screening') typeName = '검진알바';

      const perks = perksInput ? perksInput.split(',').map(s => s.trim()) : ['식사 제공', '당일지급'];

      const newJob = {
        id: 'job-' + Date.now(),
        hospital,
        regionGroup,
        location,
        title,
        type,
        typeName,
        pay,
        payAmount,
        workDate,
        workTime,
        equipment,
        perks,
        desc,
        contact,
        postedAt: '방금 전',
        timestamp: Date.now()
      };

      jobs.unshift(newJob);
      saveJobsToStorage();

      closeModal('postJobModal');
      document.getElementById('newJobForm').reset();
      renderJobList();

      showToast(`📢 "${hospital}" 신규 구인 공고가 등록되었습니다.`, 'success');
    }

    // Profile & Applications Modal
    function openProfileModal() {
      renderMyApplications();
      openModal('profileModal');
    }

    function switchProfileTab(tab) {
      const appsContent = document.getElementById('profileAppsContent');
      const infoContent = document.getElementById('profileInfoContent');
      const tabApps = document.getElementById('tabBtnApps');
      const tabInfo = document.getElementById('tabBtnInfo');

      if (tab === 'apps') {
        appsContent.classList.remove('hidden');
        infoContent.classList.add('hidden');
        tabApps.className = 'pb-2.5 px-3 border-b-2 border-brand-600 text-brand-700 transition';
        tabInfo.className = 'pb-2.5 px-3 border-b-2 border-transparent text-slate-500 hover:text-slate-800 transition';
        renderMyApplications();
      } else {
        appsContent.classList.add('hidden');
        infoContent.classList.remove('hidden');
        tabApps.className = 'pb-2.5 px-3 border-b-2 border-transparent text-slate-500 hover:text-slate-800 transition';
        tabInfo.className = 'pb-2.5 px-3 border-b-2 border-brand-600 text-brand-700 transition';
        populateProfileFields();
      }
    }

    function renderMyApplications() {
      const container = document.getElementById('profileAppsContent');
      const countEl = document.getElementById('myAppsCount');

      countEl.innerText = appliedJobs.length;

      if (appliedJobs.length === 0) {
        container.innerHTML = `
          <div class="text-center py-10 text-slate-400">
            <i data-lucide="inbox" class="w-8 h-8 mx-auto mb-2 text-slate-300"></i>
            <p class="text-xs">아직 지원한 대진 내역이 없습니다.</p>
            <p class="text-[11px] text-slate-400 mt-1">원하는 공고를 찾아 간편 지원해보세요!</p>
          </div>
        `;
        lucide.createIcons();
        return;
      }

      container.innerHTML = appliedJobs.map((app, index) => `
        <div class="p-3.5 rounded-xl border border-slate-200 bg-slate-50 flex items-start justify-between gap-3 text-xs">
          <div>
            <div class="flex items-center gap-1.5 mb-1">
              <span class="font-bold text-slate-900">${app.hospital}</span>
              <span class="px-1.5 py-0.5 rounded text-[10px] font-bold bg-emerald-100 text-emerald-800">${app.status}</span>
            </div>
            <p class="text-slate-700 font-medium line-clamp-1 mb-1">${app.title}</p>
            <div class="text-[11px] text-slate-500 space-y-0.5">
              <div>근무일: <span class="text-slate-700">${app.workDate}</span></div>
              <div>지원일시: <span class="text-slate-400">${app.appliedAt}</span></div>
            </div>
          </div>
          <button onclick="cancelApplication(${index})" class="text-[11px] text-slate-400 hover:text-rose-600 underline shrink-0">
            지원 취소
          </button>
        </div>
      `).join('');

      lucide.createIcons();
    }

    function cancelApplication(index) {
      if (confirm('대진 지원을 취소하시겠습니까?')) {
        appliedJobs.splice(index, 1);
        saveAppsToStorage();
        renderMyApplications();
        renderJobList();
        updateBadges();
        showToast('대진 지원이 취소되었습니다.', 'info');
      }
    }

    function saveUserProfile() {
      userProfile.name = document.getElementById('prefName').value.trim();
      userProfile.phone = document.getElementById('prefPhone').value.trim();
      userProfile.exp = document.getElementById('prefExp').value;
      userProfile.equip = document.getElementById('prefEquip').value.trim();
      userProfile.bio = document.getElementById('prefBio').value.trim();

      localStorage.setItem('radmatch_profile', JSON.stringify(userProfile));
      showToast('방사선사 프로필 정보가 저장되었습니다.', 'success');
    }

    function updateBadges() {
      const badge = document.getElementById('headerAppliedBadge');
      if (appliedJobs.length > 0) {
        badge.innerText = appliedJobs.length;
        badge.classList.remove('hidden');
      } else {
        badge.classList.add('hidden');
      }
    }

    function openRateInfoModal() {
      openModal('rateInfoModal');
    }

    // Reset Sample Data
    function resetSampleData() {
      if (confirm('샘플 공고 및 지원 내역 데이터를 초기화하시겠습니까?')) {
        localStorage.removeItem('radmatch_jobs');
        localStorage.removeItem('radmatch_apps');
        loadStorageData();
        renderJobList();
        updateBadges();
        showToast('데이터가 초기 상태로 복구되었습니다.', 'info');
      }
    }

    // Toast Notifications
    function showToast(message, type = 'info') {
      const container = document.getElementById('toastContainer');
      const toast = document.createElement('div');
      
      let bg = 'bg-slate-900 text-white border-slate-700';
      if (type === 'success') bg = 'bg-emerald-800 text-white border-emerald-600';
      if (type === 'warning') bg = 'bg-amber-700 text-white border-amber-500';

      toast.className = `${bg} px-4 py-2.5 rounded-xl text-xs font-semibold shadow-xl border flex items-center gap-2 transform transition-all duration-300 translate-y-3 opacity-0`;
      toast.innerHTML = `
        <i data-lucide="${type === 'success' ? 'check-circle' : 'info'}" class="w-4 h-4"></i>
        <span>${message}</span>
      `;

      container.appendChild(toast);
      lucide.createIcons();

      requestAnimationFrame(() => {
        toast.classList.remove('translate-y-3', 'opacity-0');
      });

      setTimeout(() => {
        toast.classList.add('translate-y-3', 'opacity-0');
        setTimeout(() => toast.remove(), 300);
      }, 3200);
    }
  </script>
</body>
</html>
