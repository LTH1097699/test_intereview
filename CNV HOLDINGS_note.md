_#_ complexity for `insert, delete, get, search` in single linked-list (complexitily of time and space, dont understand , just know it use node and contain next node)

_#_ complexity when insert, delete at `begin and end` of single linked-list

_#_ Khi làm web, điều gì xảy ra khi trong code gọi một lệnh redirect tới https://google.com\
_>>_ in header contains locations with https://google.com

_#_ Trong mảng phần tử đã sắp xêp, nên dùng thuật toán nào để tìm kiếm\
_>>_ is binary algorithms for search in sorted array

_#_ Find shortest path in 2 point\
_>>_ that is `dijkstra` -> when more point more time -> hoạt động với trọng số ko âm ?\
_>>_ `bellman-ford` , like dijkstra but -> hoạt động với trọng số âm, ko âm ?\
_>>_ `floyd-warshall` , more level(tầng) more time (dont understand) -> hoạt động với trọng số âm, ko âm ?

_#_ SOLID\
_>>_ dependent to abstract class, do not concrete class `(DInversion)` -> easyly to maintain, open more feature, flexiable\
_>>_ one class only have one reason to change `(Single Responsibility)` -> easy find to fix, maintain, understanable\
_>>_ `Interface Segregation Principle` (dont understand)\
_>>_ remain OL -> Open/close and L dont know

_#_ Để bảo vệ một ứng dụng web khỏi tấn công `Cross-Site Scripting (XSS)`, bạn nên áp dụng biện pháp bảo mật nào\
_>>_ Sử dụng mã hóa (Bard said) -> select\
(I miss with crsf) put an hidden id unqiue when send html to user, and check that session base on id unique (google said xss use for javascript, find more about it with xss)

_#_ Trong một chương trình có một module để tính toán điện trở và hiệu điện thế của mạch điện. Mạch điện sẽ có các linh kiện đơn như điện trở, cuộn cảm, tụ điện... và có mạch điện phức hợp gồm các mạch điện đơn hoặc phức hợp khác mắc song song hoặc nối tiếp.
Design pattern nào phù hợp nhất để thiết kế lớp cho tính năng trên\
_>>_ composite (bard said and I dont understand)

_#_ Make sure you completely understand join type (`To count the number of records in a one-to-many relationship using SQL` -> bard said left and inner, question allow both for answer -> chose inner)

_#_ How server know http is GET or POST (bard said `read fisrt word` (dont understand, may be that is format type when receive request))

_#_ Một bài toán yêu cầu tìm số thứ k nhỏ nhất trong mảng số nguyên 1 chiều không được sắp xếp. Sử dụng cấu trúc dữ liệu hoặc cách làm nào sau đây tối ưu nhất độ phức tạp về thời gian\
_>>_ inside question suggest is heap (bard said is quicksort and heap, and trie[what th fus is this] so chose heap (dont understand how it works))

_#_ complexity when get by key in Map is O(1) because it use hashtable\
_#_ complexity when check contain in Set -> because Set still work like key in Map => O(1)


_#_ give 2 class, you convert `TheirCourse` to `Course`
```java
public static class TheirCourse {
    public long id;
    public String name ;
    public List<TheirCourse> children;
}

public static class Course {
    public long id;
    public String name;
    public long parentId;
}
```
    
_=>_ answer must inside this method
```java
public List<Course> fromTheirCourses(List<TheirCourse> theirCourses) {
```

_=>_ my answer
```java
public List<Course> fromTheirCourses(List<TheirCourse> theirCourses) {
        var courses = new ArrayList<Course>();
        theirCourses.forEach(theirCourse -> {
            
            courses.add(Course.builder()
                        .id(theirCourse.getId())
                        .name(theirCourse.getName())
                        .build());

            if (theirCourse.getChildren() != null && !theirCourse.getChildren().isEmpty()) {

                var children =
                        fromTheirCourses(theirCourse.getChildren()).stream()
                        .map(child -> {
                            if (child.getParentId()!= 0) { // close for check isssue
                                return child;
                            }
                            child.setParentId(theirCourse.getId());
                            return child;
                        }).toList();
                courses.addAll(children);
            }
        });
        return courses;
    }
```

_#_ main class
```java
public static void main(String[] args) {
        var test = List.of(TheirCourse.builder()
                        .id(1L)
                        .name("course 1")
                        .build(),
                TheirCourse.builder()
                        .id(2L)
                        .name("course 2")
                        .children(List.of(TheirCourse.builder()
                                        .id(21L)
                                        .name("course 21")
                                        .build(),
                                TheirCourse.builder()
                                        .id(22L)
                                        .name("course 22")
                                        .children(List.of(TheirCourse.builder()
                                                        .id(221L)
                                                        .name("course 221")
                                                        .build(),
                                                TheirCourse.builder()
                                                        .id(222L)
                                                        .name("course 222")
                                                        .build(),
                                                TheirCourse.builder()
                                                        .id(223L)
                                                        .name("course 223")
                                                        .children(List.of(TheirCourse.builder()
                                                                        .id(2231L)
                                                                        .name("course 2231")
                                                                        .build(),
                                                                TheirCourse.builder()
                                                                        .id(2232L)
                                                                        .name("course 2232")
                                                                        .build(),
                                                                TheirCourse.builder()
                                                                        .id(2233L)
                                                                        .name("course 2233")
                                                                        .build()))
                                                        .build()))
                                        .build()))
                        .build());

        var s = fromTheirCourses(test);
    }

```

```json
[
  {
    "id": 1,
    "name": "course 1",
    "parentId": 0
  },
  {
    "id": 2,
    "name": "course 2",
    "parentId": 0
  },
  {
    "id": 21,
    "name": "course 21",
    "parentId": 2
  },
  {
    "id": 22,
    "name": "course 22",
    "parentId": 2
  },
  {
    "id": 221,
    "name": "course 221",
    "parentId": 2
  },
  {
    "id": 222,
    "name": "course 222",
    "parentId": 2
  },
  {
    "id": 223,
    "name": "course 223",
    "parentId": 2
  },
  {
    "id": 2231,
    "name": "course 2231",
    "parentId": 2
  },
  {
    "id": 2232,
    "name": "course 2232",
    "parentId": 2
  },
  {
    "id": 2233,
    "name": "course 2233",
    "parentId": 2
  }
]
```

_#_ ISSUE: when at level 3 this get id from level 1 (debug this run from level 3 and run again level 2 (recursive from this level 2 run again level 3)) (dont understand what happen)
-> dirty solution\
_=>_ check parentid != 0 return

```json
[
  {
    "id": 1,
    "name": "course 1",
    "parentId": 0
  },
  {
    "id": 2,
    "name": "course 2",
    "parentId": 0
  },
  {
    "id": 21,
    "name": "course 21",
    "parentId": 2
  },
  {
    "id": 22,
    "name": "course 22",
    "parentId": 2
  },
  {
    "id": 221,
    "name": "course 221",
    "parentId": 22
  },
  {
    "id": 222,
    "name": "course 222",
    "parentId": 22
  },
  {
    "id": 223,
    "name": "course 223",
    "parentId": 22
  },
  {
    "id": 2231,
    "name": "course 2231",
    "parentId": 223
  },
  {
    "id": 2232,
    "name": "course 2232",
    "parentId": 223
  },
  {
    "id": 2233,
    "name": "course 2233",
    "parentId": 223
  }
]
```
