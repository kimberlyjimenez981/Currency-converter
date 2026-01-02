# Currency-converter
This program performs currency conversion by taking three user inputs: the original currency, the amount to convert, and the target currency. The conversion is calculated by multiplying the input amount by the appropriate exchange rate, which is embedded in the code. The program then displays the converted amount to the user.
import java.util.HashMap;
import java.util.Map;
import java.util.Scanner;

public class Main {
  public static void main(String[] args) {

    // Create a map to store exchange rates for the different currencies.
    // All rates are relative to the US dollar.

    Map<String, Double> exchangeRates = new HashMap<>();
    exchangeRates.put("USD", 1.00);
    exchangeRates.put("EUR", 0.931262);
    exchangeRates.put("GBP", 0.807933);
    exchangeRates.put("INR", 83.152991);
    exchangeRates.put("AUD", 1.536377);
    exchangeRates.put("CAD", 1.367454);
    exchangeRates.put("SGD", 1.353669);
    exchangeRates.put("CHF", 0.897854);
    exchangeRates.put("MYR", 4.733394);
    exchangeRates.put("JPY", 149.327016);
    exchangeRates.put("CNY", 7.302885);

    // Create a scanner object for user input.

    Scanner scanner = new Scanner(System.in);
    String originalCurrency;

    // Get the original currency code from the user.
    // Keep asking until a valid currency code is provided.

    do {
      System.out.println("Enter original currency code (USD, EUR, etc.): ");
      originalCurrency = scanner.nextLine().toUpperCase();
      if (!exchangeRates.containsKey(originalCurrency)) {
        System.out.println("Invalid currency code. Please enter a valid one.");
      }
    } while (!exchangeRates.containsKey(originalCurrency));

    double amount;

    // Get the amount of money to convert.
    // Keep asking until a positive number is provided.

    do {
      System.out.println("Enter amount of money in the original currency: ");
      while (!scanner.hasNextDouble()) {
        System.out.println("That's not a number! Try again.");
        scanner.next();
      }
      amount = scanner.nextDouble();
    } while (amount <= 0);
    scanner.nextLine();

    // Get the target currency code.
    // Keep asking until a valid currency code is provided.

    String targetCurrency;
    do {
      System.out.println("Enter the currency to convert to (USD, EUR, etc.): ");
      targetCurrency = scanner.nextLine().toUpperCase();
      if (!exchangeRates.containsKey(targetCurrency)) {
        System.out.println("Invalid currency code. Please enter a valid one.");
      }
    } while (!exchangeRates.containsKey(targetCurrency));

    // Calculate the conversion rate from the original currency to the target currency.
    // This is done by converting the original currency to USD, then converting the USD to the target currency.

    double originalCurrencyToUSD = 1 / exchangeRates.get(originalCurrency);
    double usdToTargetCurrency = exchangeRates.get(targetCurrency);

    // Calculate the conversion.

    double result = amount * originalCurrencyToUSD * usdToTargetCurrency;

    // Output the final result.

    System.out.println("Amount in " + targetCurrency + ": " + result);

  }
}
