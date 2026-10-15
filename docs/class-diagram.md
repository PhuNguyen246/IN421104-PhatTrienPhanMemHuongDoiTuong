# Sơ đồ lớp — EduHub

Sơ đồ gồm 5 lớp miền chính: `Member`, `Club`, `Event`, `Registration`, `CheckIn`. Các thuộc tính định danh và khoá ngoại được thể hiện rõ; thuộc tính được đóng gói bằng `private set`, khởi tạo thông qua factory `Create(...)`.

## 1. Hình ảnh sơ đồ lớp

![Sơ đồ lớp EduHub](SoDoLopEduHub.png)

## 2. Sơ đồ Mermaid

```mermaid
classDiagram
    class Member {
        +Guid Id
        +string Name
        +string Email
        +string StudentCode
        +DateTime JoinedAt
        +MemberStatus Status
        -Member(string, string, string)
        +Create(string, string, string)$ Member
        +IsActive() bool
        +Deactivate()
        +Activate()
    }

    class Club {
        +Guid Id
        +string Name
        +string Description
        +DateTime CreatedAt
        +IReadOnlyList~Member~ Members
        -Club(string, string)
        +Create(string, string)$ Club
        +AddMember(Member)
        +RemoveMember(Guid) bool
        +ContainsMember(Guid) bool
        +MemberCount() int
    }

    class Event {
        +Guid Id
        +Guid ClubId
        +string Title
        +DateTime Date
        +int Capacity
        +bool IsOnline
        -Event(Guid, string, DateTime, int, bool)
        +Create(Guid, string, DateTime, int, bool)$ Event
        +HasCapacity(int) bool
        +RemainingCapacity(int) int
        +IsUpcoming() bool
    }

    class Registration {
        +Guid Id
        +Guid MemberId
        +Guid EventId
        +DateTime RegisteredAt
        +string Status
        -Registration(Guid, Guid)
        +Create(Guid, Guid)$ Registration
        +Confirm()
        +Cancel()
        +IsConfirmed() bool
        +IsPending() bool
        +IsCancelled() bool
    }

    class CheckIn {
        +Guid Id
        +Guid RegistrationId
        +DateTime CheckedInAt
        +string Method
        -CheckIn(Guid, string)
        +Create(Registration, string)$ CheckIn
        +Summary() string
    }

    Club "*" -- "*" Member : membership
    Club "1" --> "*" Event : ClubId FK
    Member "1" --> "*" Registration : MemberId FK
    Event "1" --> "*" Registration : EventId FK
    Registration "1" --> "0..1" CheckIn : RegistrationId FK
```

## 3. Giải thích quan hệ và khoá ngoại

- `Club` — `Member`: quan hệ nhiều-nhiều ở mức mô hình; danh sách thành viên được quản lý qua `Club.AddMember()` và chống trùng theo Id/MSSV.
- `Event.ClubId`: khoá ngoại tham chiếu `Club.Id`; một CLB có thể tổ chức nhiều sự kiện.
- `Registration.MemberId`: khoá ngoại tham chiếu `Member.Id`.
- `Registration.EventId`: khoá ngoại tham chiếu `Event.Id`. `Registration` là lớp nối thành viên với sự kiện.
- `CheckIn.RegistrationId`: khoá ngoại tham chiếu `Registration.Id`; một phiếu có tối đa một bản ghi check-in theo mô hình nghiệp vụ.
