# Migrating to the Just In Time engine

2021년 3월에 발표한 새로운 Just-in-Time 엔진이 Tailwind CSS v3.0의 클래식 엔진을 대체했습니다. 새로운 엔진은 프로젝트에 필요한 스타일을 주문형으로 생성합니다.   

Tailwind CSS v3.0 이전: 거대한 CSS파일을 생성하고, 그 파일에 이미 정의해놓은 클래스들을 가져와 사용하는 방식.   
대략 20만줄 정도 되는 클래스로 가득찬 파일을 가져와 개발 단계에서 사용하기 때문에 매우 무겁고, 배포 전에는 purge를 해줘야 해서 번거로움   

Tailwind CSS v3.0이후: 사용자가 사용하는 스타일들만 그때 그때 생성해서 사용하는 방식. 여러 클래스들을 조합해서 사용할 수 있고, 매우 가볍고, 배포 전 purge를 해주지 않아도 되서 편함   

https://tailwindcss.com/docs/upgrade-guide#migrating-to-the-jit-engine
