### Design LinkedIn

#### Requirements
1. Each member should be able to add information about their basic profile, experiences, education, skills, and accomplishments.
2. Members should be able to send or accept connection requests from other members.
3. Any member will be able to request a recommendation from other members.
4. Members should be able to create new posts to share with their connections.
5. Members should be able to add comments to posts, as well as like or share a post or comment.
6. Any member should be able to send messages to other members.
7. Members will be able to create a page for a Company and add job postings.
8. Members should be able to create groups and join any group they like.
9. Members should be able to follow other members or companies.
10. Any user of our system should be able to search for other members or companies by their name.
11. The system should be able to show basic stats about a profile, like the number of profile views, the total number of connections, and the total number of search appearances of the profile.
12. The system should send a notification to a member whenever there is a new message, connection invitation or a comment on their post.

#### Actors
1. Member
2. Admin
3. System

#### UseCases
1. Add/update profile
2. Search
3. Follow or Unfollow member or company
4. Send message
5. Create post
6. Send notifications

#### Classes
1.Member
2.Search
3.Message
4.Post
5.Comment
6. Group
7. Company
8. JobPosting
9. Notification

#### Code

1. Enums and  constant

```
public enum ConnectionInvitationStatus {
    PENDING, ACCEPTED, CONFIRMED, REJECTED, CANCELED;
}

public enum AccountStatus {
    ACTIVE, BLOCKED, BANNED, COMPROMISED, ARCHIVED, UNKNOWN;
}

public class Address {
  private String streetAddress;
  private String city;
  private String state;
  private String zipCode;
  private String country;
}
```
2. Account, Person, Member, and Admin

```
public abstract class Account {
  private String userName;
  private String password;
  private AccountStatus status;
  private Person person;

  public boolean resetPassword();
  
  public bool authenticateUser();
}

public abstract class Person {
  private String name;
  private Address address;
  private String email;
  private String phone;
  private Account account;
}

public class Member extends Person {
  Date dateOfMembership;
  String headline;
  Blob photo;
  Profile profile;
  
  boolean sendMessage() {}
  bool createPost() {}
  bool sendConnectionInvitation() {}
}

public class Admin extends Person {
  boolean blockMember() {}
  boolean unBlockMember() {}
}
```

3. Profile, Experience, etc: A member’s profile will have their job experiences, educations, skills, etc

```
class Profile {
  List<Experience> experiences;
  String summary;
  List<Education> education;
  List<Slikk> skill;
  List<Accomplishment> achievements;
  List<Recommendation> recommendation;
  
  bool addExperience() {}
}

class Experience {

}
```

4. Company and JobPosting: Companies can have multiple job postings

```
class Company {}

class JobPosting {}
```

5. Group, Post, and Message: Members can create posts, send messages, and join groups:
```
class Group {}

class Post {}

class Message {}
```

6. Search interface and SearchIndex: SearchIndex will implement the Search interface to facilitate searching for members, companies and job postings:
```
class Search {}

```

7. Notification
```
class Notification {}
```
