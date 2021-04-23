### Design Stack Overflow

Stack Overflow is one of the largest online communities for developers to learn and share their knowledge. 
The website provides a platform for its users to ask and answer questions, and through membership and active participation, 
to vote questions and answers up or down

#### System Requirements
1. Any non-member (guest) can search and view questions. However, to add or upvote a question, they have to become a member.
2. Members should be able to post new questions.
3. Members should be able to add an answer to an open question.
4. Members can add comments to any question or answer.
5. A member can upvote a question, answer or comment.
6. Members can flag a question, answer or comment, for serious problems or moderator attention.
7. Any member can add a bounty to their question to draw attention.
8. Members will earn badges for being helpful.
9. Members can vote to close a question; Moderators can close or reopen any question.
10. Members can add tags to their questions. A tag is a word or phrase that describes the topic of the question.
11. Moderators can close a question or open an already deleted question.
12. The system should also be able to identify most frequently used tags in the questions.

#### Actors
1. Admin: Mainly responsible for blocking or unblocking members.
2. Guest: All guests can search and view questions.
3. Member: add/remove questions, answers, and comments. Members can delete and un-delete their questions, answers or comments.
4. Moderator: In addition to all the activities that members can perform, moderators can close/delete/undelete any question.
5.System: Mainly responsible for sending notifications and assigning badges to members.

#### Use Cases
1. Search questions.
2. Create a new question with bounty and tags.
3. Add/modify answers to questions.
4. Add comments to questions or answers.
5. Moderators can close, delete, and un-delete any question.

#### Classes
1. Question - Title and Description to define the question, number of times a question has been viewed or voted on,status of a question.
2. Answer - Text and the view count, track the number of times an answer is voted on or flagged. 
3. Comment - text, and view, vote, and flag counts.
4. Tag -  Names and will have a field for a description to define them. Daily and weekly frequencies at which tags are associated with questions.
5. Badge - Name and Description.
6. Photo - Questions or answers can have photos
7. Bounty -  Each member, while asking a question, can place a bounty to draw attention. Bounties will have a total reputation and an expiry date.
8. Account - 4 accounts - system, guest, member, admin, and moderator. . Guests can search and view questions. Members can ask questions and earn reputation by answering questions and from bounties.
9. Notification - sending notifications to members and assigning badges to members based on their reputations.

#### Code

1. Enums, data types, and constants:

```
public enum QuestionStatus {
  OPEN, CLOSED, ON_HOLD, DELETED
}

public enum QuestionClosingRemark {
    DUPLICATE, OFF_TOPIC, TOO_BROAD, NOT_CONSTRUCTIVE, NOT_A_REAL_QUESTION, PRIMARILY_OPINION_BASED;
}

public enum AccountStatus {
    ACTIVE, CLOSED, CANCELED, BLACKLISTED, BLOCKED;
}

public class Address {
  private String streetAddress;
  private String city;
  private String state;
  private String zipCode;
  private String country;
}

```

2. Account, Member, Admin, and Moderator : 
* Classes represent the different people that interact with our system.

```
class Account {
  int id;
  String password;
  String name;
  Address address;
  String email;
  int phone;
  AccountStatus status; //AccountStatus.Active
  int reputation;//0
  
  public boolean resetPassword();
}

class Member {
  private Account account;
  
  public int getReputation() {
    return this.account.reputation;
  }
  
  public String getEmail() {
    return this.account.email;
  }
  
  public Question createQuestion(String question) {
    
  }
  
  public Tag createTag() {
  }
}

class Admin extends Member {
  public String blockMember(Member member) {}
  
  public string unblockMember(Member member) {}
}


class Moderator extends Member {
  public String closeQuestion(Question question) {}
  
  public String OpenQuestion(Question question) {}
}

```

3. Badge, Tag, and Notification: 
* Members have badges, questions have tags and notifications:

```
class Badge {
  private String name;
  private String description;
}

class Tag {
  String name;
  String description
  int dailyfrequancy = 0;
  int weeklyfrequency = 0;
}

class Notification {
  int notificationId;
  Date createdon; //Date.NOW();
  String content;
  
  public Notification sendNotification() {
  }
}
```

4. Photo and Bounty:
* Members can put bounties on questions. Answers and Questions can have multiple photos.

```
class Photo {
  int id;
  String path
  Member member;
  
  public void delete(Photo photo) { 
  }
}

class Bounty {
  int reputation;
  Date expiry;
  
  public void modifyRetutation(reputation) {}
}
```

5. Question, Comment and Answer:
* Members can ask questions, as well as add an answer to any question. All members can add comments to all open questions or answers:

```
class Question {
  String title;
  String description; 
  int viewCount;
  int voteCount;
  Date creationTime;
  Date updateTime;
  QuestionStatue status; //OPEN
  QuestionClosingRemark closeingremark; //DUPLICATE
  
  Bounty bounty;
  Member askingMember;
  Photo[] photos;
  Comments[] comments;
  Answer[] answers;
  
  public void close() {}
  public void open() {}
  public Comment addComment(Comment comment) {}
  public Bounty addBounty(Bounty bounty) {}
  public List<Question> search(String query) {}
}

class Comment {
  String text;
  Date creation;
  int flagCount;
  int voteCount;
  Member askingmember;
  
  public int incrementVoteCount() {
    this.voteCount+=1;
  }
}

class Answer {
  String answerText;
  bool accepted;
  int voteCount;
  int flagCount;
  Date create;
  Member createmember;
  Photo[] photos;
  
  public void incrementVoteCount() {
    this.voteCount++;
  }
}

```

https://github.com/tssovi/grokking-the-object-oriented-design-interview/blob/master/object-oriented-design-case-studies/design-stack-overflow.md
