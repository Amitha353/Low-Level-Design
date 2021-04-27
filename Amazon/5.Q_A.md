Amazon QA application

```
import java.util.*;

public class OOPDesignQnA {

    Map> questionAnswerMap;


    Map questionMap;
    Map> productQnAMap;
    Map> productQuestions;

    public OOPDesignQnA(){
        this.questionMap = new TreeMap<>();
        this.productQnAMap = new TreeMap<>();
    }


    public void addQuestion(String text, Integer productId, Integer userId){
        Question question = new Question(productId, text, userId);
        questionMap.put(question.id, question);
        productQnAMap.put(productId, questionMap);
        if(productQuestions.containsKey(productId)) {
            List list = productQuestions.get(productId);
            list.add(question);
            Collections.sort(list);
        }else{
            List questions = new ArrayList<>();
            questions.add(question);
            productQuestions.put(productId, questions);
        }
    }

    public void addAnswer(Integer productId, Integer questionId, String text, Integer userId){
        Answer answer = new Answer(questionId, productId, text, userId);
        Question question = questionMap.get(questionId);
        List answerList = question.answerList;
        answerList.add(answer);
        Collections.sort(answerList);

        if(questionAnswerMap.containsKey(question)){
            questionAnswerMap.get(question).put(answer.id, answer);
        }else{
            Map answerMap = new HashMap<>();
            answerMap.put(answer.id, answer);
            questionAnswerMap.put(question, answerMap);
        }
    }

    public List getAllQuestions(Integer productId){
        return productQuestions.get(productId);
    }

    public List getAnswersforQuestions(Integer productId, Integer questionId){
        Map qMap = productQnAMap.get(productId);
        return qMap.get(questionId).answerList;
    }

    public void upvoteQuestion(Integer productId, Integer questionId){
        Map qMap = productQnAMap.get(productId);
        qMap.get(questionId).upvotes += 1;
        List questions = productQuestions.get(productId);
        Collections.sort(questions);
    }

    public void upvoteAnswer(Integer productId, Integer questionId, Integer answerId){
        Map qMap = productQnAMap.get(productId);
        Question question = qMap.get(questionId);
        Answer answer = questionAnswerMap.get(question).get(answerId);
        answer.upvotes += 1;
        Collections.sort(question.answerList);
    }



}

class Question implements Comparable{

    static Integer count = 0;

    Integer id;
    Integer productId;
    String text;
    Integer userId;
    List answerList;
    Integer upvotes;
    Date createdAt;


    public Question(Integer productId, String text, Integer userId){
        this.productId = productId;
        this.text = text;
        this.userId= userId;
        this.id = count++;
        answerList = new ArrayList<>();
        this.upvotes = 0;
        this.createdAt = new Date();
    }

    @Override
    public int compareTo(Question o) {
        if(this.upvotes == o.upvotes){
            return createdAt.compareTo(o.createdAt);
        }else{
            return this.upvotes.compareTo(o.upvotes);
        }
    }

}


class Answer implements Comparable{

    static Integer count = 0;

    Integer id; // Do I need this ?
    Integer questionId;
    Integer productId;
    Integer userId;
    String text;
    Integer upvotes;
    Date createdAt;


    public Answer(Integer questionId, Integer productId, String text, Integer userId){
        this.questionId = questionId;
        this.productId = productId;
        this.text = text;
        this.userId = userId;
        this.id = count++;
        this.upvotes = 0;
        this.createdAt = new Date();
    }

    @Override
    public int compareTo(Answer o) {
        if(this.upvotes == o.upvotes){
            return createdAt.compareTo(o.createdAt);
        }else{
            return this.upvotes.compareTo(o.upvotes);
        }
    }
}
```

https://leetcode.com/discuss/interview-question/object-oriented-design/125119/Design-QandA-application-as-in-Amazon-has-it-for-each-product

https://howtodoinjava.com/java8/sort-stream-multiple-fields/

```
//first name comparator
Comparator<Employee> compareByFirstName = Comparator.comparing( Employee::getFirstName );
 
//last name comparator
Comparator<Employee> compareByLastName = Comparator.comparing( Employee::getLastName );
 
//Compare by first name and then last name (multiple fields)
Comparator<Employee> compareByFullName = compareByFirstName.thenComparing(compareByLastName);
 
//Using Comparator - pseudo code
list.stream().sorted( comparator ).collect();


public class Main 
{
    public static void main(String[] args) 
    {
        ArrayList<Employee> employees = getUnsortedEmployeeList();
         
        //Compare by first name and then last name
        Comparator<Employee> compareByName = Comparator
                                                .comparing(Employee::getFirstName)
                                                .thenComparing(Employee::getLastName);
         
        List<Employee> sortedEmployees = employees.stream()
                                        .sorted(compareByName)
                                        .collect(Collectors.toList());
         
        System.out.println(sortedEmployees);
    }
    
```
