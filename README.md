import java.util.Scanner;
public class CurrencyConverter {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        System.out.println("Welcome to the Currency Converter!");
        String[] currencies = {"USD", "EUR", "GBP", "INR"};
        System.out.println("Available currencies:");
        for (int i = 0; i < currencies.length; i++) {
            System.out.println((i + 1) + ". " + currencies[i]);
        }
        System.out.print("Enter the number for the currency to convert from: ");
        int fromCurrencyIndex = scanner.nextInt() - 1;
        
        System.out.print("Enter the number for the currency to convert to: ");
        int toCurrencyIndex = scanner.nextInt() - 1;

        if (fromCurrencyIndex < 0 || fromCurrencyIndex >= currencies.length ||
            toCurrencyIndex < 0 || toCurrencyIndex >= currencies.length) {
            System.out.println("Invalid currency selection. Please try again.");
            return;
        }

        String fromCurrency = currencies[fromCurrencyIndex];
        String toCurrency = currencies[toCurrencyIndex];

        System.out.print("Enter the amount to convert: ");
        double amount = scanner.nextDouble();

        double convertedAmount = convertCurrency(fromCurrency, toCurrency, amount);
        
        if (convertedAmount != -1) {
            System.out.printf("Converted Amount: %.2f %s\n", convertedAmount, toCurrency);
        } else {
            System.out.println("Conversion rate not available.");
        }

        scanner.close();
    }
    public static double convertCurrency(String from, String to, double amount) {
        double rate = getConversionRate(from, to);
        if (rate == -1) {
            return -1; 
        }
        return amount * rate;
    }
    public static double getConversionRate(String from, String to) {
        if (from.equals("USD") && to.equals("EUR")) return 0.85;
        if (from.equals("USD") && to.equals("GBP")) return 0.75;
        if (from.equals("USD") && to.equals("INR")) return 74.50;
        if (from.equals("EUR") && to.equals("USD")) return 1.18;
        if (from.equals("EUR") && to.equals("GBP")) return 0.88;
        if (from.equals("EUR") && to.equals("INR")) return 87.50;
        if (from.equals("GBP") && to.equals("USD")) return 1.33;
        if (from.equals("GBP") && to.equals("EUR")) return 1.14;
        if (from.equals("GBP") && to.equals("INR")) return 100.50;
        if (from.equals("INR") && to.equals("USD")) return 0.013;
        if (from.equals("INR") && to.equals("EUR")) return 0.011;
        if (from.equals("INR") && to.equals("GBP")) return 0.0099;
        
        return -1;
    }
}
