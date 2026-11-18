# flutter_note

SQLite에 저장하는 메모 앱입니다. 클린 아키텍처(data / domain / presentation)를 적용했습니다.

## 기능
- 메모 추가 · 수정
- 삭제 후 스낵바에서 실행 취소
- 날짜 / 제목, 오름차순 / 내림차순 정렬

## 구조
- `data` — `NoteDbHelper` (sqflite), `NoteRepositoryImpl`
- `domain` — `Note`(Freezed), `NoteOrder`, UseCase 5종(조회·단건·추가·수정·삭제)
- `presentation` — `NotesViewModel` + `NotesEvent/State`, `AddEditNoteViewModel`

## 실행
```bash
flutter pub get
dart run build_runner build --delete-conflicting-outputs
flutter run
flutter test        # sqflite_common_ffi 로 DB 테스트
```
