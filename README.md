# Flutter Clean Architecture

Flutter에서 **클린 아키텍처**를 두 개의 앱에 적용하며 계층 분리와 테스트를 익힌 저장소입니다.

| 앱 | 설명 | 사용한 것 |
| :--- | :--- | :--- |
| **flutter_note** | SQLite에 저장하는 메모 앱. 추가·수정·삭제(실행 취소), 날짜/제목 정렬 | sqflite, Freezed, Provider, ChangeNotifier |
| **search_image** | Pixabay API로 이미지를 검색하는 앱. 로딩·에러 상태 처리 | http, Freezed, Provider, Stream 기반 UI 이벤트 |

## 구조

두 앱 모두 같은 3계층 구조를 사용합니다.

```
lib/
├── data/          # 외부와 통신하는 구현 (DB 헬퍼, HTTP API, Repository 구현체)
├── domain/        # 앱의 규칙 (모델, Repository 인터페이스, UseCase)
└── presentation/  # 화면과 상태 (ViewModel, State, Event, Widget)
```

- **domain** 은 Flutter에 의존하지 않습니다. 화면이나 DB를 바꿔도 규칙은 그대로입니다.
- **presentation** 은 UseCase만 알고, DB나 API를 직접 부르지 않습니다.
- 의존성은 `di/provider_setup.dart` 한 곳에서 조립합니다.

## 실행

```bash
cd flutter_note        # 또는 cd search_image
flutter pub get
dart run build_runner build --delete-conflicting-outputs   # Freezed 코드 생성
flutter run
```

## 테스트

```bash
cd flutter_note  && flutter test    # NoteDbHelper (sqflite_common_ffi)
cd search_image  && flutter test    # HomeViewModel + 가짜 Repository
```

## 배운 것

- 상태를 `State` 객체 하나로 관리하고 `copyWith` 로만 바꾸면, 화면이 어떤 상태인지 한눈에 보입니다.
- 실패를 `Result.success / Result.error` 로 값으로 다루면, ViewModel에서 try/catch 대신 화면에 보여 줄 메시지를 결정할 수 있습니다.
- Repository를 인터페이스로 두면 가짜 구현으로 화면 로직을 테스트할 수 있습니다.
