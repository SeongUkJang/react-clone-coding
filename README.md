# project-react-clone-coding

React를 이용하여 Clone-coding을 구현해보았습니다.

### **1. App.jsx** - 메인 애플리케이션 구성 🌐

```jsx
javascript
복사편집
import './App.scss' // 스타일 시트 불러오기
import Topbanner from './components/Topbanner' // 상단 배너 컴포넌트
import Hero from './components/Hero' // 히어로 섹션 컴포넌트
import { useState } from 'react' // 상태 관리 위한 useState 훅
import Header from './components/Header' // 헤더 컴포넌트
import Section1 from './components/Section1' // 첫 번째 섹션 컴포넌트
import Section2 from './components/Section2' // 두 번째 섹션 컴포넌트
import Section3 from './components/Section3' // 세 번째 섹션 컴포넌트
import Section4 from './components/Section4' // 네 번째 섹션 컴포넌트
import Footer from './components/Footer' // 푸터 컴포넌트

// 메인 애플리케이션 컴포넌트
function App() {
  // 상태 설정: topBanner
  const [topBanner, setTopBanner] = useState('')

  // 상단 배너를 올리는 함수
  const upTopBanner = ()=> {
    setTopBanner('up')
  }

  return (
    // 'app-container' 클래스에 topBanner 상태 값에 따라 클래스 추가
    <div className={`app-container ${topBanner}`}>
      <Topbanner onClick={upTopBanner} /> {/* 상단 배너 */}
      <Header /> {/* 헤더 */}
      <Hero /> {/* 히어로 섹션 */}
      <Section1 /> {/* 첫 번째 섹션 */}
      <Section2 /> {/* 두 번째 섹션 */}
      <Section3 /> {/* 세 번째 섹션 */}
      <Section4 /> {/* 네 번째 섹션 */}
      <Footer /> {/* 푸터 */}
    </div>
  )
}

export default App

```

**설명**:

- **상태 관리**: `useState`를 사용해 `topBanner` 상태를 관리하고 있습니다. 배너 클릭 시 상단 배너를 올리는 효과를 주기 위해 `setTopBanner`를 활용합니다.
- **컴포넌트 구조**: `Topbanner`, `Header`, `Hero`, `Section1`, `Section2`, `Section3`, `Section4`, `Footer` 컴포넌트를 각각 임포트하고 JSX로 구성하여 전체 웹 페이지를 만듭니다.

---

### **2. Topbanner.jsx** - 상단 배너 (슬라이드 효과) 🎥

```jsx
javascript
복사편집
import React from 'react' // React 불러오기
import './styles/Topbanner.scss' // 스타일 시트 불러오기
import { Swiper, SwiperSlide } from 'swiper/react' // Swiper 슬라이드 라이브러리
import { Autoplay } from 'swiper/modules' // 자동 전환 기능
import 'swiper/css' // Swiper 기본 스타일

// 상단 배너 컴포넌트
const Topbanner = ({ onClick }) => {
  return (
    <div className='top_banner'>
      {/* Swiper 슬라이드 */}
      <Swiperdirection='vertical' // 슬라이드 방향: 세로
        slidesPerView={1} // 한 번에 보여지는 슬라이드 수
        loop={true} // 무한 루프
        autoplay={{delay: 3000}} // 자동 전환, 3초마다 슬라이드 전환
        modules={[Autoplay]} // 자동 전환 모듈
        className='tb_slider'
      >
        {/* 각 슬라이드 내용 */}
        <SwiperSlide>
          <a href="#">Join now and get free shipping!</a>
        </SwiperSlide>
        <SwiperSlide>
          <a href="#">Enjoy free shipping on all purchases</a>
        </SwiperSlide>
        <SwiperSlide>
          <a href="#">Gift wrapping, exclusive gift message card benefits.</a>
        </SwiperSlide>
      </Swiper>
      {/* 닫기 버튼 */}
      <div className="close" onClick={onClick}>Click</div>
    </div>
  )
}

export default Topbanner

```

**설명**:

- **슬라이드 효과**: `Swiper` 라이브러리를 사용해 세로 방향으로 자동 슬라이드가 이루어지며, 3초마다 전환됩니다.
- **닫기 버튼**: 사용자가 배너를 닫을 수 있도록 `onClick` 이벤트로 상위 컴포넌트에서 전달된 함수를 호출합니다.

---

### **3. Header.jsx** - 페이지 상단 헤더 & 네비게이션 🌐

```jsx
javascript
복사편집
import React, { useEffect, useState } from 'react' // React 및 훅 불러오기
import './styles/Header.scss' // 스타일 시트 불러오기
import Nav from './Nav' // 네비게이션 컴포넌트
import Util from './Util' // 유틸리티 컴포넌트

// 헤더 컴포넌트
const Header = () => {
  const [isScrolled, setIsScrolled] = useState(false) // 스크롤 여부 상태

  // 스크롤 이벤트 처리
  useEffect(() => {
    const handleScroll = () => {
      const scrollTop = window.scrollY
      setIsScrolled(scrollTop > 0) // 스크롤이 0 이상이면 isScrolled를 true로 설정
    }

    // 스크롤 이벤트 리스너 추가
    window.addEventListener('scroll', handleScroll)
    return () => window.removeEventListener('scroll', handleScroll) // 클린업
  }, [])

  return (
    <header className={isScrolled ? 'scroll' : ''}>
      <div className="inner">
        <Nav /> {/* 네비게이션 */}
        <h1 className="logo">
          <a href="#">
            <img src="/img/Aesop_logo2.svg" alt="logo" />
          </a>
        </h1>
        <Util /> {/* 유틸리티 */}
      </div>
    </header>
  )
}

export default Header

```

**설명**:

- **스크롤 이벤트**: `window.scrollY` 값을 통해 페이지가 스크롤된 여부를 확인하고, 이를 바탕으로 헤더의 클래스가 변경됩니다.
- **`isScrolled` 상태**: 스크롤 여부에 따라 헤더의 스타일을 다르게 적용해, 페이지가 스크롤되었을 때 상단에 고정되는 효과를 주게 됩니다.

---

### **4. Section1.jsx** - 첫 번째 섹션 (부드러운 애니메이션 효과) 🌟

```jsx
javascript
복사편집
import React, { useEffect } from 'react' // React 및 효과 훅 불러오기
import Aos from 'aos' // AOS 애니메이션 라이브러리
import 'aos/dist/aos.css' // AOS CSS 불러오기
import './styles/Section1.scss' // 스타일 시트 불러오기

// 첫 번째 섹션 컴포넌트
const Section1 = () => {
  useEffect(() => {
    Aos.init({ duration: 1000 }) // AOS 애니메이션 초기화, 지속 시간 설정
  }, [])

  return (
    <section className='sc1'>
      <div className="inner">
        <div className="img-wrap" data-aos="fade-right"> {/* 오른쪽에서 왼쪽으로 페이드 인 */}
          <img src="/img/Aesop1.gif" alt="intro" />
        </div>
        <div className="t-wrap" data-aos="fade-left"> {/* 왼쪽에서 오른쪽으로 페이드 인 */}
          <h2 className="con_tit">
            Enriched cleansing <br /> with Eleos Nourishing Body Cleanser
          </h2>
          <p className="txt">
            With its soft texture and woody, spicy, and herbal scent, Eleos Nourishing Body Cleanser
            fills your shower space with a sensual and enjoyable experience.
          </p>
          <a href="#" className="con_btn black">
            <span>Read More</span>
            <p>→</p>
          </a>
        </div>
      </div>
    </section>
  )
}

export default Section1

```

**설명**:

- **AOS 애니메이션**: `Aos.init`을 통해 스크롤 시 텍스트와 이미지를 부드럽게 나타나게 하는 효과를 주고 있습니다. `data-aos` 속성을 사용하여 각 요소에 애니메이션을 적용합니다.

---

### **5. Section2.js** - 두 번째 섹션 (슬라이드 쇼 + 자동 전환) 🎥

```jsx
javascript
복사편집
import React, { useRef, useEffect } from 'react' // React, useRef 및 useEffect 불러오기
import './styles/Section2.scss' // 스타일 시트 불러오기
import Aos from 'aos' // AOS 애니메이션 라이브러리
import 'aos/dist/aos.css' // AOS 스타일
import { Swiper, SwiperSlide } from 'swiper/react' // Swiper 슬라이드 라이브러리
import { Navigation, Pagination } from 'swiper/modules' // 내비게이션 및 페이지네이션 기능
import 'swiper/css' // Swiper 기본 스타일
import 'swiper/css/navigation' // 내비게이션 스타일
import 'swiper/css/pagination' // 페이지네이션 스타일
import sc2Data from '../data/sc2Data' // 데이터 파일 불러오기

// 두 번째 섹션 컴포넌트
const Section2 = () => {

  // 슬라이드의 이전/다음 버튼을 위한 ref 설정
  const prevRef = useRef(null)
  const nextRef = useRef(null)
  const swiperRef = useRef(null)

  // AOS 애니메이션 초기화
  useEffect(() => {
    Aos.init({duration: 1000}) // 애니메이션 지속 시간 설정
  }, [])

  // Swiper의 내비게이션을 설정하는 useEffect 훅
  useEffect(() => {
    if (swiperRef.current &&
    swiperRef.current.params &&
    prevRef.current &&
    nextRef.current) {
      swiperRef.current.params.navigation.prevEl = prevRef.current
      swiperRef.current.params.navigation.nextEl = nextRef.current
      swiperRef.current.navigation.destroy() // 기존 내비게이션 파괴
      swiperRef.current.navigation.init() // 내비게이션 초기화
      swiperRef.current.navigation.update() // 내비게이션 업데이트
    }
  }, [])

  return (
    <section className='sc2'>
      <div className="inner" data-aos="fade-up"> {/* AOS 애니메이션 */}
        <div className="t-wrap">
          <h2 className="con_tit">Aesop Fragrances</h2>
          <p className="txt_2">Eau De Parfum</p>
        </div>

        {/* Swiper 슬라이더 설정 */}
        <SwiperslidesPerView={3} // 한 번에 3개의 슬라이드 표시
          modules={[Navigation, Pagination]} // 내비게이션과 페이지네이션 모듈 사용
          className='s2_slider'
          onSwiper={(swiper) => (swiperRef.current = swiper)} // swiper 인스턴스를 ref에 저장
          pagination={{ type: 'progressbar' }} // 페이지네이션을 진행 표시줄로 설정
          loop={true} // 무한 루프 활성화
        >
          {sc2Data.map((item) => (
            <SwiperSlide key={item.id}>
              <a href="#">
                <div className="info-wrap">
                  <div className='s2-btn'>{item.title}</div>
                  <div className='name'>{item.name}</div>
                </div>
                <div className="img-wrap">
                  <img src={item.image} alt="img" />
                </div>
                <div className="ml">{item.ml}</div>
                <div className="cost">{item.cost}</div>
              </a>
            </SwiperSlide>
          ))}
        </Swiper>

        {/* 커스텀 내비게이션 버튼 */}
        <button className='custom-prev' ref={prevRef} type='button' />
        <button className='custom-next' ref={nextRef} type='button' />
      </div>
    </section>
  )
}

export default Section2

```

**설명**:

- **슬라이드 기능**: `Swiper`를 사용하여 이미지 슬라이드를 구현합니다. 한 번에 3개의 슬라이드가 보이며, 좌우 버튼으로 슬라이드를 제어합니다. `Pagination`을 사용해 진행 표시줄이 나타납니다.
- **AOS 애니메이션**: `data-aos="fade-up"` 속성으로 페이지가 로드될 때 부드러운 애니메이션 효과가 적용됩니다.

---

### **6. Section3.js** - 세 번째 섹션 (슬라이드 쇼) 🌳

```jsx
javascript
복사편집
import React, {useEffect} from 'react' // React 및 useEffect 훅
import Aos from 'aos' // AOS 애니메이션 라이브러리
import 'aos/dist/aos.css' // AOS 스타일
import './styles/Section3.scss' // 스타일 시트 불러오기
import { Swiper, SwiperSlide } from 'swiper/react' // Swiper 슬라이드 라이브러리
import 'swiper/css' // Swiper 기본 스타일

// 세 번째 섹션 컴포넌트
const Section3 = () => {

  // AOS 애니메이션 초기화
  useEffect(() => {
    Aos.init({duration: 1000}) // 애니메이션 지속 시간 설정
  }, [])

  // 슬라이드 클래스 배열
  const slideClasses = [
    's3_sl_1',
    's3_sl_2',
    's3_sl_3',
    's3_sl_4'
  ]

  return (
    <section className='sc3'>
      <div className="inner">
        <div className="t-wrap" data-aos="fade-right">
          <h2 className="con_tit">Subtle Transition</h2>
          <p className="txt">
            Of the five senses, the sense of smell is most closely linked to memory. <br />
            Aesop’s fragrance range evokes the lush green forests of Japan, the bustle of traditional Moroccan markets, and the landscapes of the Mediterranean coast.
          </p>
          <a href="#" className="con_btn black">
            <span>Discover Eau de Parfum</span>
            <p>→</p>
          </a>
        </div>
        <div className="s3_sl_wrap" data-aos="fade-left">
          <div className="in">
            <SwiperspaceBetween={30} // 슬라이드 간 간격
              slidesPerView={1} // 한 번에 1개의 슬라이드 표시
              breakpoints={{ 1024: { slidesPerView: 2 } }} // 1024px 이상 화면에서는 2개 슬라이드 표시
              loop={true} // 무한 루프
            >
              {slideClasses.map((slide, index) => (
                <SwiperSlide key={index}>
                  <div className={slide}></div> {/* 각 슬라이드 클래스 */}
                </SwiperSlide>
              ))}
            </Swiper>
          </div>
        </div>
      </div>
    </section>
  )
}

export default Section3

```

**설명**:

- **슬라이드 구성**: `Swiper`를 사용하여 슬라이드를 구현합니다. 화면 크기에 따라 슬라이드의 개수를 동적으로 변경할 수 있습니다.
- **AOS 애니메이션**: `data-aos="fade-left"` 속성을 사용하여 섹션 내 요소들이 부드럽게 왼쪽에서 오른쪽으로 등장하는 애니메이션을 적용합니다.

---

### **7. Section4.js** - 네 번째 섹션 (Instagram Feed) 📸

```jsx
javascript
복사편집
import React, { useEffect } from 'react' // React 및 useEffect 훅
import './styles/Section4.scss' // 스타일 시트 불러오기
import instaData from '../data/instaData' // Instagram 데이터 파일 불러오기
import Aos from 'aos' // AOS 애니메이션 라이브러리
import 'aos/dist/aos.css' // AOS 스타일

// 네 번째 섹션 컴포넌트
const Section4 = () => {
  useEffect(() => {
    Aos.init({duration: 1000}) // AOS 애니메이션 초기화
  }, [])

  return (
    <section className='sc4'>
      <div className="inner">
        <div className="t-wrap">
          <h2 className="con_tit">Instagram</h2>
          <p className="txt_5">@Aesop</p>
        </div>
        <ul className='s4_lst'>
          {instaData.map((data, index) => (
            <lidata-aos="fade-up" // AOS 애니메이션 (업 방향으로 나타남)
              data-aos-delay={data.delay} // 각 이미지의 딜레이 시간 설정
              key={index}
            >
              <a href="#">
                <img src={data.src} alt={`img-${index}`} />
              </a>
            </li>
          ))}
        </ul>
      </div>
    </section>
  )
}

export default Section4

```

**설명**:

- **Instagram 피드**: `instaData`를 통해 Instagram 이미지들을 불러와서 리스트 형태로 표시합니다. 각 이미지에는 `data-aos="fade-up"`를 적용해 스크롤 시 부드럽게 위로 나타나는 애니메이션 효과를 주고 있습니다.
- **AOS 애니메이션**: 각 Instagram 이미지에 딜레이를 두어 조금씩 시간차를 두고 이미지들이 나타나도록 설정했습니다.

---

### **8. Footer.jsx** - 페이지 하단 푸터 🏠

```jsx
javascript
복사편집
import React from 'react' // React 불러오기
import './styles/Footer.scss' // 스타일 시트 불러오기
import { footerCenterMenu, footerCompany, footerInfoLinks, snsIcons, customerCenter } from '../data/footerData'

// 푸터 컴포넌트
const Footer = () => {
  return (
    <footer>
      <div className="inner">
        <div className="left">
          <h3>
            <img src={footerCompany.logo} alt="logo" />
          </h3>
          <p className="foot_txt1">
            Company Name: {footerCompany.CompanyName} <br />
            Representative: {footerCompany.Representative} <br />
            Address: {footerCompany.Address} <br/>
            Business Registration Number: {footerCompany.BusinessRegistrationNumber} <br />
            Mail Order Business Report Number: {footerCompany.MailOrderBusinessReportNumber} <br />
            Hosting Provider: {footerCompany.HostingProvider} <br />
            Main Phone: {footerCompany.MainPhone}, Main Email: {footerCompany.MainEmail}
          </p>
          <p className="foot_txt2">{footerCompany.copyright}</p>
        </div>
        <ul className="center">
          {footerCenterMenu.map((menu, idx) => (
            <li key={idx}>
              <a href="#">{menu.title}</a>
              <ul>
                {menu.links.map((link, i) => (
                  <li key={i}>
                    <a href="#">{link}</a>
                  </li>
                ))}
              </ul>
            </li>
          ))}
        </ul>
        <div className="right">
          <p className="foot_txt3">Customer Center</p>
          <div className="tel">{customerCenter.tel}</div>
          <a href="#" className="talk_btn">1 : 1 Talk</a>
        </div>
      </div>
      <div className="inner">
        <div className="info">
          {footerInfoLinks.map((link, i) => (
            <a href={link.href} key={i}>{link.text}</a>
          ))}
        </div>
        <div className="sns">
          {snsIcons.map((icon, i) => (
            <a href="#" key={i}>
              <img src={icon.src} alt={icon.alt} />
            </a>
          ))}
        </div>
      </div>
    </footer>
  )
}

export default Footer

```

**설명**:

- **푸터 구성**: 회사 정보, 고객센터, SNS 링크를 포함한 여러 섹션으로 푸터를 구성합니다.
- *`footerData.js`*에서 데이터를 가져와서 푸터를 동적으로 렌더링합니다.
