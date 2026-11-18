# search_image

Pixabay API로 이미지를 검색하는 앱입니다. 클린 아키텍처와 테스트를 함께 연습했습니다.

## 기능
- 검색어 입력 → 이미지 목록 표시
- 로딩 상태 표시, 실패 시 스낵바 안내

## 구조
- `data` — `PixabayApi`(http), `Result`, `PhotoApiRepoImpl`
- `domain` — `Photo`, `PhotoApiRepo`(인터페이스), `GetPhotosUseCase`
- `presentation` — `HomeViewModel`(`ChangeNotifier` + `Stream<HomeUiEvent>`), `HomeState`

## 실행
```bash
flutter pub get
dart run build_runner build --delete-conflicting-outputs
flutter run
flutter test
```

> Pixabay 키는 데모용 공개 키라 그대로 두었습니다. 실제 배포 시에는 `--dart-define` 으로 분리하는 것을 권합니다.
