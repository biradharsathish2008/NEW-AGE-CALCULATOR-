import java.time.*;
import java.time.temporal.ChronoUnit;
import java.time.format.TextStyle;
import java.util.Locale;
import java.util.Scanner;

public class AdvancedAgeCalculator {

    // -------------------------------------------------------
    // VALIDATION FUNCTION
    // -------------------------------------------------------
    public static boolean isValidDate(int y, int m, int d) {
        if (y <= 0 || m <= 0 || d <= 0) return false;

        try {
            LocalDate input = LocalDate.of(y, m, d);
            if (input.isAfter(LocalDate.now())) return false;
            return true;
        } catch (Exception e) {
            return false;
        }
    }

    // -------------------------------------------------------
    // AGE CATEGORY
    // -------------------------------------------------------
    public static String getAgeCategory(int years) {
        if (years < 13) return "Child";
        else if (years < 20) return "Teen";
        else if (years < 60) return "Adult";
        else return "Senior";
    }

    // -------------------------------------------------------
    // HEALTH SUGGESTION (SAFE)
    // -------------------------------------------------------
    public static String healthSuggestion(String category) {
        switch (category) {
            case "Child":
                return "Stay active and playful!";
            case "Teen":
                return "Focus on studies and healthy habits.";
            case "Adult":
                return "Balance work and personal life.";
            case "Senior":
                return "Stay socially connected and keep moving.";
            default:
                return "Have a great day!";
        }
    }

    // -------------------------------------------------------
    // ZODIAC SIGN
    // -------------------------------------------------------
    public static String getZodiacSign(int day, int month) {
        if ((month == 1 && day >= 20) || (month == 2 && day <= 18)) return "Aquarius";
        if ((month == 2 && day >= 19) || (month == 3 && day <= 20)) return "Pisces";
        if ((month == 3 && day >= 21) || (month == 4 && day <= 19)) return "Aries";
        if ((month == 4 && day >= 20) || (month == 5 && day <= 20)) return "Taurus";
        if ((month == 5 && day >= 21) || (month == 6 && day <= 20)) return "Gemini";
        if ((month == 6 && day >= 21) || (month == 7 && day <= 22)) return "Cancer";
        if ((month == 7 && day >= 23) || (month == 8 && day <= 22)) return "Leo";
        if ((month == 8 && day >= 23) || (month == 9 && day <= 22)) return "Virgo";
        if ((month == 9 && day >= 23) || (month == 10 && day <= 22)) return "Libra";
        if ((month == 10 && day >= 23) || (month == 11 && day <= 21)) return "Scorpio";
        if ((month == 11 && day >= 22) || (month == 12 && day <= 21)) return "Sagittarius";
        return "Capricorn";
    }

    // -------------------------------------------------------
    // BIRTH MONTH FACTS
    // -------------------------------------------------------
    public static String getBirthMonthFacts(int month) {
        switch (month) {
            case 1: return "January — known for new beginnings and winter season.";
            case 2: return "February — month of uniqueness and short celebrations.";
            case 3: return "March — linked with spring and fresh bloom.";
            case 4: return "April — known for pleasant weather and freshness.";
            case 5: return "May — the month of early summer and vibrant nature.";
            case 6: return "June — famous for summer and long days.";
            case 7: return "July — month of warm weather and holidays.";
            case 8: return "August — known for late summer and festivals.";
            case 9: return "September — known for autumn beginnings and calm weather.";
            case 10: return "October — famous for cool weather and harvest season.";
            case 11: return "November — a month known for autumn and festivals.";
            case 12: return "December — known for winter and celebrations.";
            default: return "Unknown month.";
        }
    }

    // -------------------------------------------------------
    // DAY OF WEEK (NEW)
    // -------------------------------------------------------
    public static String getDayOfWeek(LocalDate dob) {
        DayOfWeek day = dob.getDayOfWeek();
        return day.getDisplayName(TextStyle.FULL, Locale.ENGLISH).toUpperCase();
    }

    // -------------------------------------------------------
    // LUCKY NUMBER (sum of ALL DOB digits)
    // -------------------------------------------------------
    public static int luckyNumber(int d, int m, int y) {
        int total = d + m + y;
        int sum = 0;

        while (total > 0) {
            sum += total % 10;
            total /= 10;
        }
        return sum;
    }

  
    // AGE ON OTHER PLANETS
    // -------------------------------------------------------
    public static void ageOnPlanets(int earthYears) {
        System.out.println("\n--- AGE ON OTHER PLANETS ---");
        System.out.println("Mercury: " + (earthYears / 0.24));
        System.out.println("Mars: " + (earthYears / 1.88));
        System.out.println("Jupiter: " + (earthYears / 11.86));
    }

    // -------------------------------------------------------
    // LEAP YEAR CHECK
    // -------------------------------------------------------
    public static void checkLeapYearBirth(LocalDate dob) {
        if (Year.isLeap(dob.getYear())) {
            System.out.println("You were born in a leap year.");
        } else {
            System.out.println("You were NOT born in a leap year.");
        }

        if (dob.getMonthValue() == 2 && dob.getDayOfMonth() == 29) {
            System.out.println("Your birthday occurs once every 4 years (29 FEB).");
        }
    }

    // -------------------------------------------------------
    // NEXT BIRTHDAY COUNTDOWN
    // -------------------------------------------------------
    public static void nextBirthdayCountdown(LocalDate dob) {
        LocalDate today = LocalDate.now();
        LocalDate nextBirthday = dob.withYear(today.getYear());

        if (nextBirthday.isBefore(today) || nextBirthday.equals(today)) {
            nextBirthday = nextBirthday.plusYears(1);
        }

        Period diff = Period.between(today, nextBirthday);

        if (diff.getMonths() == 0 && diff.getDays() == 0) {
            System.out.println("🎉 Today is your Birthday! 🎂");
        } else {
            System.out.println("Next Birthday in: " + diff.getMonths() + " months " + diff.getDays() + " days");
        }
    }

    // -------------------------------------------------------
    // AGE IN DIFFERENT UNITS
    // -------------------------------------------------------
    public static void ageInUnits(LocalDate dob) {
        LocalDate today = LocalDate.now();

        long days = ChronoUnit.DAYS.between(dob, today);
        long hours = days * 24;
        long minutes = hours * 60;
        long seconds = minutes * 60;

        System.out.println("\n--- AGE IN DIFFERENT UNITS ---");
        System.out.println("Days Lived: " + days);
        System.out.println("Hours Lived: " + hours);
        System.out.println("Minutes Lived: " + minutes);
        System.out.println("Seconds Lived: " + seconds);
    }

    // -------------------------------------------------------
    // MAIN PROGRAM
    // -------------------------------------------------------
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        System.out.println("Enter Date of Birth:");
        System.out.print("Day: ");
        int d = sc.nextInt();
        System.out.print("Month: ");
        int m = sc.nextInt();
        System.out.print("Year: ");
        int y = sc.nextInt();

        if (!isValidDate(y, m, d)) {
            System.out.println("\n❌ Invalid Date Entered! Please enter a valid past date.");
            return;
        }

        LocalDate dob = LocalDate.of(y, m, d);
        LocalDate today = LocalDate.now();

        Period age = Period.between(dob, today);

        System.out.println("\n--- AGE DETAILS ---");
        System.out.println("Age: " + age.getYears() + " Years, " + age.getMonths() + " Months, " + age.getDays() + " Days");

        // Age category + health suggestion
        String category = getAgeCategory(age.getYears());
        System.out.println("Age Category: " + category);
        System.out.println("Health Tip: " + healthSuggestion(category));

        // Zodiac Sign
        System.out.println("Zodiac Sign: " + getZodiacSign(d, m));

        // Month Facts
        System.out.println("Birth Month Facts: " + getBirthMonthFacts(m));

        // Day of Birth (NEW)
        System.out.println("You were born on a " + getDayOfWeek(dob));

        // Lucky Number (NEW)
        System.out.println("Your Fun Lucky Number: " + luckyNumber(d, m, y));

        // Age on Planets (NEW)
        ageOnPlanets(age.getYears());

        // Leap Year
        checkLeapYearBirth(dob);

        // Next Birthday
        nextBirthdayCountdown(dob);

        // Units
        ageInUnits(dob);
    }
}
