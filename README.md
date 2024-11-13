# java-code-of-project

// Import necessary packages
import java.util.ArrayList;
import java.util.List;

// User class
class User {
    private String name;
    private int age;
    private double weight;
    private double height;

    public User(String name, int age, double weight, double height) {
        this.name = name;
        this.age = age;
        this.weight = weight;
        this.height = height;
    }

    public String getName() { return name; }
    public int getAge() { return age; }
    public double getWeight() { return weight; }
    public double getHeight() { return height; }

    public double calculateBMI() {
        return weight / (height * height);
    }
}

// Workout class
class Workout {
    private String workoutType;
    private int duration; // in minutes
    private double caloriesBurned;

    public Workout(String workoutType, int duration, double caloriesBurned) {
        this.workoutType = workoutType;
        this.duration = duration;
        this.caloriesBurned = caloriesBurned;
    }

    public String getWorkoutType() { return workoutType; }
    public int getDuration() { return duration; }
    public double getCaloriesBurned() { return caloriesBurned; }
}

// FitnessTracker class
class FitnessTracker {
    private User user;
    private List<Workout> workouts;
    private double dailyCalorieGoal;

    public FitnessTracker(User user, double dailyCalorieGoal) {
        this.user = user;
        this.workouts = new ArrayList<>();
        this.dailyCalorieGoal = dailyCalorieGoal;
    }

    public void addWorkout(Workout workout) {
        workouts.add(workout);
    }

    public double getTotalCaloriesBurned() {
        return workouts.stream().mapToDouble(Workout::getCaloriesBurned).sum();
    }

    public boolean hasMetCalorieGoal() {
        return getTotalCaloriesBurned() >= dailyCalorieGoal;
    }

    public void showProgress() {
        System.out.println("User: " + user.getName());
        System.out.println("Total Calories Burned: " + getTotalCaloriesBurned());
        System.out.println("Calorie Goal Met: " + hasMetCalorieGoal());
    }
}

// Main class
public class FitnessApp {
    public static void main(String[] args) {
        User user = new User("saurav", 19, 75.0, 1.75);
        FitnessTracker tracker = new FitnessTracker(user, 500); // Daily goal of 500 calories

        // Add workouts
        tracker.addWorkout(new Workout("Running", 30, 300));
        tracker.addWorkout(new Workout("Cycling", 45, 250));

        // Show progress
        tracker.showProgress();
    }
}
