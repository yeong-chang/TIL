# CRUD란?

CRUD 가 뭘까….

Create(생성)

```java
// 예: 새 사용자 추가
public void createUser(User user) {
    userRepository.save(user); // 데이터베이스에 새로운 사용자 저장
}
```

Read(조회)

```java
// 예: 특정 사용자 조회
public User getUserById(Long id) {
    return userRepository.findById(id).orElse(null); // 데이터베이스에서 특정 사용자 조회
}
```

Update(수정)

```java
// 예: 사용자 정보 수정
public void updateUser(Long id, User user) {
    if (userRepository.existsById(id)) {
        user.setId(id); 
        userRepository.save(user); // 데이터베이스에서 사용자 정보 업데이트
    }
}
```

Delete(삭제)

```java
// 예: 사용자 삭제
public void deleteUser(Long id) {
    userRepository.deleteById(id); // 데이터베이스에서 특정 사용자 삭제
}
```