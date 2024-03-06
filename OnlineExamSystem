import java.util.HashMap;
import java.util.Map;
import java.util.Scanner;
import java.util.Timer;
import java.util.TimerTask;

class User {
    private String username;
    private String password;
    private String fullName;
    private int score;

    public User(String username, String password, String fullName) {
        this.username = username;
        this.password = password;
        this.fullName = fullName;
        this.score = 0;
    }

    public String getUsername() {
        return username;
    }

    public String getPassword() {
        return password;
    }

    public String getFullName() {
        return fullName;
    }

    public int getScore() {
        return score;
    }

    public void updateProfile(String newFullName, String newPassword) {
        this.fullName = newFullName;
        this.password = newPassword;
        System.out.println("Profile updated successfully.");
    }

    public void increaseScore() {
        score++;
    }
}

class Question {
    private String question;
    private Map<String, Boolean> options;

    public Question(String question, Map<String, Boolean> options) {
        this.question = question;
        this.options = options;
    }

    public String getQuestion() {
        return question;
    }

    public Map<String, Boolean> getOptions() {
        return options;
    }
}

class Exam {
    private Map<Integer, Question> questions;
    private int currentQuestionNumber;

    public Exam() {
        this.questions = new HashMap<>();
        initializeQuestions();
        this.currentQuestionNumber = 1;
    }

    private void initializeQuestions() {
        // Populate questions and options
        // Add more questions and options as needed
        Map<String, Boolean> options1 = new HashMap<>();
        options1.put("A. Option 1", true);
        options1.put("B. Option 2", false);
        options1.put("C. Option 3", false);
        questions.put(1, new Question("What is the capital of France?", options1));

        Map<String, Boolean> options2 = new HashMap<>();
        options2.put("A. Option 1", false);
        options2.put("B. Option 2", true);
        options2.put("C. Option 3", false);
        questions.put(2, new Question("What is the largest planet in our solar system?", options2));
    }

    public Question getNextQuestion() {
        return questions.get(currentQuestionNumber++);
    }
}

class TimerManager {
    private Timer timer;
    private int timeRemaining;

    public TimerManager(int timeLimitInMinutes) {
        this.timer = new Timer();
        this.timeRemaining = timeLimitInMinutes * 60;
        scheduleTimerTask();
    }

    private void scheduleTimerTask() {
        timer.scheduleAtFixedRate(new TimerTask() {
            public void run() {
                if (timeRemaining > 0) {
                    System.out.println("Time remaining: " + timeRemaining + " seconds");
                    timeRemaining--;
                } else {
                    System.out.println("Time's up! Auto-submitting answers...");
                    // Implement auto-submit logic here
                    timer.cancel();
                }
            }
        }, 1000, 1000);
    }

    public void stopTimer() {
        timer.cancel();
    }
}

public class OnlineExamSystem {
    private static User currentUser;
    private static Exam exam;
    private static TimerManager timerManager;

    public static void main(String[] args) {
        initializeUsers();
        login();
        displayMenu();
    }

    private static void initializeUsers() {
        // Add sample users
        // Replace this with a database or other persistent storage in a real-world scenario
        User user1 = new User("user1", "password1", "John Doe");
        User user2 = new User("user2", "password2", "Jane Doe");

        Map<String, User> users = new HashMap<>();
        users.put(user1.getUsername(), user1);
        users.put(user2.getUsername(), user2);
    }

    private static void login() {
        Scanner scanner = new Scanner(System.in);

        while (true) {
            System.out.print("Enter username: ");
            String username = scanner.nextLine();
            System.out.print("Enter password: ");
            String password = scanner.nextLine();

            if (validateUser(username, password)) {
                System.out.println("Login successful. Welcome, " + currentUser.getFullName() + "!");
                break;
            } else {
                System.out.println("Invalid username or password. Please try again.");
            }
        }
    }

    private static boolean validateUser(String username, String password) {
        // Replace with a database lookup or other user authentication logic
        Map<String, User> users = new HashMap<>();
        users.put("user1", new User("user1", "password1", "John Doe"));
        users.put("user2", new User("user2", "password2", "Jane Doe"));

        User user = users.get(username);
        if (user != null && user.getPassword().equals(password)) {
            currentUser = user;
            return true;
        }

        return false;
    }

    private static void displayMenu() {
        Scanner scanner = new Scanner(System.in);

        while (true) {
            System.out.println("\nOnline Exam Menu:");
            System.out.println("1. Update Profile and Password");
            System.out.println("2. Start Exam");
            System.out.println("3. Logout");
            System.out.print("Enter your choice: ");
            int choice = scanner.nextInt();

            switch (choice) {
                case 1:
                    updateProfile();
                    break;
                case 2:
                    startExam();
                    break;
                case 3:
                    System.out.println("Logout successful. Goodbye!");
                    System.exit(0);
                default:
                    System.out.println("Invalid choice. Please choose again.");
            }
        }
    }

    private static void updateProfile() {
        Scanner scanner = new Scanner(System.in);

        System.out.print("Enter new full name: ");
        String newFullName = scanner.nextLine();
        System.out.print("Enter new password: ");
        String newPassword = scanner.nextLine();

        currentUser.updateProfile(newFullName, newPassword);
    }

    private static void startExam() {
        // Replace with exam setup logic, e.g., selecting an exam type or category
        exam = new Exam();
        timerManager = new TimerManager(10); // 10 minutes time limit for the exam

        Scanner scanner = new Scanner(System.in);

        while (true) {
            Question question = exam.getNextQuestion();
            displayQuestion(question);

            System.out.print("Enter your answer: ");
            String userAnswer = scanner.nextLine();

            // Replace with answer validation logic
            validateAnswer(question, userAnswer);

            if (examFinished()) {
                break;
            }
        }

        // Exam is finished, stop the timer
        timerManager.stopTimer();
    }

    private static void displayQuestion(Question question) {
        System.out.println("\n" + question.getQuestion());
        for (String option : question.getOptions().keySet()) {
            System.out.println(option);
        }
    }

    private static void validateAnswer(Question question, String userAnswer) {
        Map<String, Boolean> options = question.getOptions();
        for (Map.Entry<String, Boolean> entry : options.entrySet()) {
            if (entry.getKey().startsWith(userAnswer) && entry.getValue()) {
                System.out.println("Correct answer! +1 point");
                currentUser.increaseScore();
                break;
            } else {
                System.out.println("Incorrect answer. No points awarded.");
                break;
            }
        }
    }

    private static boolean examFinished() {
        // Replace with logic to check if all questions have been answered
        return false;
    }
}
