<script setup>
import { ref, computed } from 'vue'

const currentDay = ref(0)

const itinerary = [
  {
    day: 'Day 1',
    date: 'Arrival & Naha',
    type: 'schedule',
    schedule: [
      { time: '07:00~07:30', activity: '抵達高雄小港機場(順便吃東西沒有飛機餐)', icon: '✈️', link: '' },
      { time: '10:10', activity: '高雄小港機場起飛', icon: '✈️', link: '' },
      { time: '13:00', activity: '那霸機場 (拿行李+坐接駁車到OTS臨空豐崎營業所取車)', icon: '✈️', link: 'https://www.google.com/maps/search/?api=1&query=Naha+Airport' },
      { time: '15:00', activity: '取車 (OTS臨空豐崎營業所)', icon: '🚗', link: 'https://www.google.com/maps/search/?api=1&query=OTS臨空豐崎營業所' },
      { time: '15:30', activity: '開車出發', icon: '💨' },
      { time: '15:45', activity: '波上宮', icon: '⛩️', link: 'https://www.google.com/maps/search/?api=1&query=Naminoue+Shrine' },
      { time: '17:00', activity: '出發', icon: '💨' },
      { time: '18:00', activity: '找晚餐 (美國村)', icon: '🎡', link: 'https://www.google.com/maps/search/?api=1&query=American+Village+Okinawa' },
      { time: '20:00', activity: '出發', icon: '💨' },
      { time: '20:30', activity: '民宿 Okinawa Kona Garden', icon: '🏠', link: 'https://www.google.com/maps/search/?api=1&query=沖繩,%20宇流麻,%20石川東恩納１５６４−２' },
    ]
  },
  {
    day: 'Day 2',
    date: 'Aquarium & Beef',
    type: 'schedule',
    schedule: [
      { time: '09:30', activity: '出發', icon: '🚗' },
      { time: '11:20', activity: '美麗海水族館 (午餐預計吃INOH海景餐廳)', icon: '🐋', link: 'https://www.google.com/maps/search/?api=1&query=Okinawa+Churaumi+Aquarium' },
      { time: '17:00', activity: '回程', icon: '↩️' },
      { time: '18:30', activity: '燒肉 琉球の牛恩納別館', icon: '🥩', link: 'https://www.google.com/maps/search/?api=1&query=Ryukyu+no+Ushi+Onna' },
      { time: '20:00', activity: '出發', icon: '💨' },
      { time: '20:20', activity: '民宿', icon: '🏠', link: 'https://www.google.com/maps/search/?api=1&query=沖繩,%20宇流麻,%20石川東恩納１５６４−２' },
    ]
  },
  {
    day: 'Day 3',
    date: 'Zoo & Seafood',
    type: 'schedule',
    schedule: [
      { time: '09:30', activity: '出發', icon: '🚗' },
      { time: '10:40', activity: '兒童王國', icon: '🦁', link: 'https://www.google.com/maps/search/?api=1&query=Okinawa+Zoo+%26+Museum' },
      { time: '16:00', activity: '出發', icon: '💨' },
      { time: '16:20', activity: '泡瀨漁港 (晚餐)', icon: '🦞', link: 'https://www.google.com/maps/search/?api=1&query=泡瀨漁港' },
      { time: '18:00', activity: '出發', icon: '💨' },
      { time: '19:00', activity: '民宿 check in (Chura Gahna House Tsubogawa Naha)', icon: '🏨', link: 'https://www.google.com/maps/search/?api=1&query=Chura+Gahna+House+Tsubogawa+Naha' },
    ]
  },
  {
    day: 'Day 4',
    date: 'Shopping & Park',
    type: 'schedule',
    schedule: [
      { time: '09:00', activity: '出發', icon: '🚗' },
      { time: '09:40', activity: '沖繩安良波公園', icon: '🏞️', link: 'https://www.google.com/maps/search/?api=1&query=Ginowan+Seaside+Park' },
      { time: '12:00', activity: '出發', icon: '💨' },
      { time: '12:20', activity: 'PARCO CITY (萬代扭蛋)', icon: '🛍️', link: 'https://www.google.com/maps/search/?api=1&query=PARCO+CITY+Okinawa' },
      { time: '17:00', activity: '出發', icon: '💨' },
      { time: '17:40', activity: '民宿 (Chura Gahna House Tsubogawa Naha)(可不回去民宿直接去國際通)', icon: '🏨', link: 'https://www.google.com/maps/search/?api=1&query=Chura+Gahna+House+Tsubogawa+Naha' },
      { time: '18:30', activity: '國際通吃晚餐逛街', icon: '🍜', link: 'https://www.google.com/maps/search/?api=1&query=Kokusai-dori' },
    ]
  },
  {
    day: 'Day 5',
    date: 'Culture & Depature',
    type: 'schedule',
    schedule: [
      { time: '10:00', activity: '出發', icon: '🚗' },
      { time: '10:20', activity: '達摩寺', icon: '🏯', link: 'https://www.google.com/maps/search/?api=1&query=Daruma+Temple+Okinawa' },
      { time: '11:00', activity: '出發', icon: '💨' },
      { time: '11:30', activity: '玉泉洞', icon: '💧', link: 'https://www.google.com/maps/search/?api=1&query=Gyokusendo+Cave' },
      { time: '14:00', activity: '出發', icon: '💨' },
      { time: '14:30', activity: 'iias 沖繩豐崎 (萬代扭蛋+DDM)', icon: '🛍️', link: 'https://www.google.com/maps/search/?api=1&query=iias+Okinawa+Toyosaki' },
      { time: '17:00', activity: '出發', icon: '💨' },
      { time: '17:15', activity: 'OTS臨空豐崎營業所', icon: '🚗', link: 'https://www.google.com/maps/search/?api=1&query=OTS臨空豐崎營業所' },
      { time: '18:00', activity: '前到那霸機場', icon: '✈️', link: 'https://www.google.com/maps/search/?api=1&query=Naha+Airport' },
    ]
  },
  {
    day: '景點',
    date: 'Must Visit',
    type: 'gallery',
    regions: [
      {
        name: '地圖',
        places: [
          { name: 'Okinawa Churaumi Aquarium', image: 'https://bobbyfun.tw/wp-content/uploads/2025/06/20250815004726_0_032993.jpg' },
        ]
      }
    ]
  },
  {
    day: 'Map Code',
    date: 'Navigation Info',
    type: 'mapcodes',
    codes: [
      { name: '那霸機場 (Naha Airport)', code: '33 123 404', note: 'Day 1 & 5' },
      { name: 'OTS臨空豐崎營業所 (OTS Rent-a-car)', code: '232 543 542*63', note: 'Day 1 & 5' },
      { name: '波上宮 (Naminoue Shrine)', code: '33 185 023*55', note: 'Day 1' },
      { name: '美國村 (American Village)', code: '33 526 450*65', note: 'Day 1' },
      { name: '美麗海水族館 (Churaumi Aquarium)', code: '553 075 797*77', note: 'Day 2' },
      { name: '燒肉 琉球の牛 恩納店', code: '206 096 716', note: 'Day 2' },
      { name: '兒童王國 (Okinawa Zoo & Museum)', code: '33 561 798*88', note: 'Day 3' },
      { name: '泡瀨漁港 (Awase Fish Market)', code: '33 565 310', note: 'Day 3' },
      { name: '宜野灣海濱公園 (Ginowan Seaside Park)', code: '33 403 300*83', note: 'Day 4' },
      { name: 'PARCO CITY', code: '33 308 868*53', note: 'Day 4' },
      { name: '國際通 (Kokusai Dori)', code: '33 157 444*60', note: 'Day 4' },
      { name: '達摩寺 (Daruma Temple)', code: '33 161 597*46', note: 'Day 5' },
      { name: '玉泉洞 (Gyokusendo)', code: '232 495 333*86', note: 'Day 5' },
      { name: 'iias 沖繩豐崎', code: '232 543 368*63', note: 'Day 5' },
    ]
  },
  {
    day: '餐廳',
    date: 'Dining Plan',
    type: 'restaurants',
    days: [
      {
        dayTitle: 'Day 1',
        rows: [
          { 
            time: '晚餐(參考)', 
            restaurant: '塔可飯咖啡(Taco Rice Cafe)', 
            address: '沖縄県中頭郡北谷町美浜9-1 (Depot Island C棟 2F)', 
            note: 'Mapcode: 33 526 450*63' 
          },
          { 
            time: '晚餐(參考)', 
            restaurant: '迴轉壽司市場-美浜店', 
            address: '沖縄県中頭郡北谷町美浜2-4-3', 
            note: 'Mapcode: 33 526 489*78' 
          },
          { 
            time: '晚餐(參考)', 
            restaurant: 'A&W 漢堡-美浜店', 
            address: '沖縄県中頭郡北谷町美浜15-69 (Carnival Park Mihama 2F)', 
            note: 'Mapcode: 33 526 317*74' 
          },
        ]
      },
      {
        dayTitle: 'Day 2',
        rows: [
          { 
            time: '午餐', 
            restaurant: 'INOH海景餐廳(吃到飽)', 
            address: '美麗海水族館 4樓',
            note: 'MapCode：553 075 797*74' 
          },
          { 
            time: '晚餐(建議訂位)', 
            restaurant: '燒肉 琉球の牛 恩納店-別館', 
            address: '沖縄県国頭郡恩納村前兼久101', 
            note: '建議搜尋「前兼久101」或使用MapCode：206 096 716' 
          }
        ]
      },
      {
        dayTitle: 'Day 3',
        rows: [
          { 
            time: '早餐+午餐(帶去沖繩王國吃)', 
            restaurant: 'lawson 便利商店', 
            address: '251-1 Ishikawa Higashionna, Uruma, Okinawa 904-1111日本', 
            note: 'MapCode：33 895 250*74' 
          },
          { 
            time: '午餐(沖繩王國自己找東西吃)', 
            restaurant: '', 
            address: '', 
            note: 'MapCode：' 
          },
          { 
            time: '晚餐', 
            restaurant: '泡瀨漁港', 
            address: '904-2172 沖縄県沖縄市泡瀬1-11-34', 
            note: 'MapCode：33 565 341*02' 
          }
          
        ]
      },
      {
        dayTitle: 'Day 4',
        rows: [
          { 
            time: '午餐', 
            restaurant: 'PARCO CITY', 
            address: '沖縄県浦添市西洲3丁目1-1', 
            note: 'MapCode：33 339 276 ' 
          },
          { 
            time: '晚餐(參考)', 
            restaurant: '國際通-暖暮拉麵', 
            address: '', 
            note: '聽說很多人' 
          },
          { 
            time: '晚餐(參考)', 
            restaurant: '國際通-琉家拉麵', 
            address: '', 
            note: 'MapCode： ' 
          },
          { 
            time: '晚餐(參考)', 
            restaurant: '國際通-一蘭拉麵', 
            address: '', 
            note: ' ' 
          },
          { 
            time: '晚餐(參考)', 
            restaurant: '國際通-國際通屋台村', 
            address: '', 
            note: '營業時間：11:00〜01：00  日本路邊攤 看起來位子不多' 
          },
          { 
            time: '晚餐(參考)', 
            restaurant: '國際通-麥當勞', 
            address: '', 
            note: '' 
          }
        ]
      },
      {
        dayTitle: 'Day 5',
        rows: [
          { 
            time: '午餐', 
            restaurant: '玉泉洞', 
            address: '', 
            note: 'MapCode： ' 
          },
          { 
            time: '晚餐(參考)', 
            restaurant: '那霸機場(3F)-牛排屋88', 
            address: '', 
            note: '33 123 404' 
          },
          { 
            time: '晚餐(參考)', 
            restaurant: '那霸機場(4F)-吉野家 Ｘ 花丸烏龍麵', 
            address: '', 
            note: '' 
          },
          { 
            time: '晚餐(參考)', 
            restaurant: '那霸機場(3F)-A&W漢堡', 
            address: '', 
            note: '' 
          }
          
        ]
      }
    ]
  }
]

const currentItem = computed(() => itinerary[currentDay.value])
</script>

<template>
  <div class="min-h-screen bg-slate-950 text-slate-50 font-sans selection:bg-purple-500/30">
    <!-- Background Elements -->
    <div class="fixed inset-0 overflow-hidden pointer-events-none -z-10">
      <div class="absolute top-[-10%] left-[-10%] w-[50vw] h-[50vw] bg-purple-600/20 rounded-full blur-[120px]"></div>
      <div class="absolute bottom-[-10%] right-[-10%] w-[50vw] h-[50vw] bg-blue-600/20 rounded-full blur-[120px]"></div>
    </div>

    <div class="w-[80vw] mx-auto px-4 py-12 min-h-screen flex flex-col">
      <!-- Header -->
      <header class="text-center mb-12 animate-fade-in">
        <h1 class="text-4xl md:text-5xl font-extrabold bg-clip-text text-transparent bg-gradient-to-r from-teal-400 via-blue-500 to-purple-500 mb-4 drop-shadow-sm tracking-tight">
          沖繩旅遊行程 🌴
        </h1>
      </header>

      <!-- Tabs Navigation -->
      <div class="flex flex-wrap justify-center gap-2 mb-10 p-1 bg-white/5 backdrop-blur-md rounded-2xl border border-white/10 mx-auto w-full md:w-auto">
        <button
          v-for="(item, index) in itinerary"
          :key="index"
          @click="currentDay = index"
          class="relative px-5 py-2.5 rounded-xl text-sm font-medium transition-all duration-300 outline-none focus:ring-2 focus:ring-blue-500/50"
          :class="currentDay === index ? 'text-white shadow-lg shadow-blue-500/25' : 'text-slate-400 hover:text-white hover:bg-white/5'"
        >
          <div v-if="currentDay === index" class="absolute inset-0 bg-gradient-to-r from-blue-600 to-purple-600 rounded-xl -z-10 opacity-100 transition-opacity"></div>
          <span class="relative z-10">{{ item.day }}</span>
        </button>
      </div>

      <!-- Main Content Area -->
      <main class="flex-1">
        <div class="relative bg-white/5 backdrop-blur-xl border border-white/10 rounded-3xl p-6 md:p-8 shadow-2xl overflow-hidden transition-all duration-500" :key="currentDay">
          <!-- Decorative Header for Card -->
          <div class="flex items-end justify-between mb-8 border-b border-white/10 pb-4">
            <div>
              <h2 class="text-2xl font-bold text-white mb-1">{{ currentItem.day }}</h2>
            </div>
            <div class="hidden md:block opacity-20 text-6xl">
              {{ currentItem.type === 'gallery' ? '📸' : '🏖️' }}
            </div>
          </div>

          <!-- Schedule View -->
          <div v-if="currentItem.type === 'schedule'" class="relative space-y-0">
            <!-- Vertical Line -->
            <div class="absolute left-[27px] top-4 bottom-4 w-0.5 bg-gradient-to-b from-blue-500/50 via-purple-500/50 to-transparent"></div>

            <div 
              v-for="(item, idx) in currentItem.schedule" 
              :key="idx" 
              class="relative flex group items-start gap-6 py-4 transition-all duration-300 hover:translate-x-1"
            >
              <!-- Time & Icon -->
              <div class="flex flex-col items-center flex-shrink-0 w-14 z-10">
                <a 
                  v-if="item.link" 
                  :href="item.link" 
                  target="_blank"
                  class="w-14 h-14 rounded-2xl bg-slate-900 border border-white/10 flex items-center justify-center text-2xl shadow-lg group-hover:scale-110 group-hover:border-blue-500/50 transition-all duration-300 relative cursor-pointer"
                >
                   <div class="absolute inset-0 bg-blue-500/10 rounded-2xl opacity-0 group-hover:opacity-100 transition-opacity"></div>
                   {{ item.icon }}
                </a>
                <div 
                  v-else
                  class="w-14 h-14 rounded-2xl bg-slate-900 border border-white/10 flex items-center justify-center text-2xl shadow-lg group-hover:scale-110 group-hover:border-blue-500/50 transition-all duration-300 relative"
                >
                  <div class="absolute inset-0 bg-blue-500/10 rounded-2xl opacity-0 group-hover:opacity-100 transition-opacity"></div>
                  {{ item.icon }}
                </div>
              </div>
              
              <!-- Content -->
              <div class="flex-1 pt-2">
                <span class="inline-block px-2 py-0.5 rounded-md bg-white/5 text-blue-300 text-xs font-mono mb-1 border border-white/5">
                  {{ item.time }}
                </span>
                
                <a 
                  v-if="item.link" 
                  :href="item.link" 
                  target="_blank"
                  class="block text-slate-200 text-lg leading-snug font-medium group-hover:text-white transition-colors hover:text-blue-400 hover:underline decoration-blue-500/30 underline-offset-4"
                >
                   {{ item.activity }} <span class="text-sm opacity-50 ml-1">↗</span>
                </a>
                <p 
                  v-else
                  class="text-slate-200 text-lg leading-snug font-medium group-hover:text-white transition-colors"
                >
                  {{ item.activity }}
                </p>
              </div>
            </div>
          </div>

          <!-- Gallery View -->
          <div v-else-if="currentItem.type === 'gallery'" class="space-y-8">
            <div v-for="region in currentItem.regions" :key="region.name" class="animate-fade-in">
              <h3 class="text-xl font-bold text-transparent bg-clip-text bg-gradient-to-r from-blue-300 to-purple-300 mb-4 pl-2 border-l-4 border-blue-500/50">
                {{ region.name }}
              </h3>
              <div class="grid grid-cols-1 gap-4">
                <div 
                  v-for="place in region.places" 
                  :key="place.name"
                  class="group relative rounded-xl overflow-hidden bg-slate-800 border border-white/10 shadow-lg"
                >
                  <img 
                    :src="place.image" 
                    :alt="place.name"
                    class="w-full h-auto transition-transform duration-700 ease-in-out"
                    loading="lazy"
                  />
                </div>
              </div>
            </div>
          </div>

          <!-- Map Codes View -->
          <div v-else-if="currentItem.type === 'mapcodes'" class="overflow-x-auto animate-fade-in">

            <div>
              map code 查詢網址: <a href="https://www.mapion.co.jp/" target="blank">https://www.mapion.co.jp/</a>
            </div>

            <table class="w-full text-left border-collapse">
              <thead>
                <tr class="border-b border-white/10 text-slate-300">
                  <th class="py-4 px-4 font-bold">名稱 (Name)</th>
                  <th class="py-4 px-4 font-bold text-right text-nowrap">Map Code</th>
                </tr>
              </thead>
              <tbody class="divide-y divide-white/5">
                <tr 
                  v-for="(code, idx) in currentItem.codes" 
                  :key="idx"
                  class="group hover:bg-white/5 transition-colors"
                >
                  <td class="py-3 px-4 text-slate-200 font-medium group-hover:text-white transition-colors">
                    {{ code.name }}
                    <span v-if="code.note" class="block text-xs text-slate-500 font-normal mt-1">{{ code.note }}</span>
                  </td>
                  <td class="py-3 px-4 text-right font-mono text-lg text-emerald-300 group-hover:text-emerald-200 tracking-wider">
                    {{ code.code }}
                  </td>
                </tr>
              </tbody>
            </table>
          </div>

          <!-- Restaurant View -->
          <div v-else-if="currentItem.type === 'restaurants'" class="space-y-8 animate-fade-in">

            <div v-for="(dayData, dayIndex) in currentItem.days" :key="dayIndex" class="bg-slate-900/50 backdrop-blur-sm rounded-2xl p-6 border border-white/5 shadow-inner">
              <h3 class="text-xl font-bold text-transparent bg-clip-text bg-gradient-to-r from-orange-300 to-rose-300 mb-6 pl-3 border-l-4 border-orange-500/50 flex items-center gap-2">
                {{ dayData.dayTitle }}
                <span v-if="!dayData.rows || dayData.rows.length === 0" class="text-xs font-normal text-slate-500 border border-slate-700 px-2 py-0.5 rounded-full bg-slate-800">No Reservations</span>
              </h3>
              
              <div class="overflow-x-auto rounded-xl border border-white/5">
                <table class="w-full text-left border-collapse bg-slate-900/30">
                  <thead class="bg-white/5">
                    <tr class="text-slate-300 text-sm">
                      <th class="py-3 px-4 font-semibold min-w-[150px] border-b border-white/10">時間</th>
                      <th class="py-3 px-4 font-semibold min-w-[200px] border-b border-white/10">餐廳</th>
                      <th class="py-3 px-4 font-semibold min-w-[200px] border-b border-white/10">地址</th>
                      <th class="py-3 px-4 font-semibold min-w-[200px] border-b border-white/10">備註</th>
                    </tr>
                  </thead>
                  <tbody class="divide-y divide-white/5">
                    <tr v-if="!dayData.rows || dayData.rows.length === 0">
                        <td colspan="3" class="py-6 text-center text-slate-500 italic">
                          No restaurants planned for this day
                        </td>
                    </tr>
                    <tr 
                      v-else
                      v-for="(row, rIdx) in dayData.rows" 
                      :key="rIdx"
                      class="group hover:bg-white/5 transition-colors"
                    >
                      <td class="py-3 px-4 text-orange-300 font-mono text-sm group-hover:text-orange-200">
                        {{ row.time }}
                      </td>
                      <td class="py-3 px-4 text-slate-200 font-medium group-hover:text-white transition-colors">
                        {{ row.restaurant }}
                      </td>
                      <td class="py-3 px-4 text-slate-400 text-sm group-hover:text-slate-300">
                        {{ row.address }}
                      </td>
                      <td class="py-3 px-4 text-slate-400 text-sm group-hover:text-slate-300">
                        {{ row.note }}
                      </td>
                    </tr>
                  </tbody>
                </table>
              </div>
            </div>
          </div>

        </div>
      </main>

      <footer class="mt-12 text-center text-slate-600 text-sm">
        Travel better, together.
      </footer>
    </div>
  </div>
</template>

<style scoped>
.animate-fade-in {
  animation: fadeIn 0.8s ease-out forwards;
}

@keyframes fadeIn {
  from { opacity: 0; transform: translateY(-20px); }
  to { opacity: 1; transform: translateY(0); }
}
</style>
