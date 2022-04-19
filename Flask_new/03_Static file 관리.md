# Static file 관리

**Static file**: Javascript, CSS, 이미지 파일 등

- Static 폴더에 저장한다.

#### url_for 함수

- 프로젝트 도중 경로가 바뀔 때 코드를 바꿀 필요가 없음

```html
<link rel="stylesheet" href="{{ url_for('static', filename='css/style.css') }}">
```

