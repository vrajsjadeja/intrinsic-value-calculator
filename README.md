# intrinsic-value-calculator
A Python tool to calculate the intrinsic value of NSE-listed equities using the DCF model.
class IntrinsicValueCalculator:
   
    
    def __init__(self, current_bond_yield: float):
        """
        Initializes the calculator with the current AAA corporate bond yield.
        """
        self.current_bond_yield = current_bond_yield

    def calculate_graham_value(self, eps: float, growth_rate: float) -> float:
        """
        Calculates intrinsic value.
        Formula: V = (EPS * (8.5 + 2 * Growth Rate) * 4.4) / Current Yield
        """
        # 8.5 is the assumed P/E ratio for a no-growth company
        base_pe = 8.5 
        # 4.4 was the average yield of high-grade corporate bonds in Graham's time
        historic_yield_multiplier = 4.4 
        
        intrinsic_value = (eps * (base_pe + 2 * growth_rate) * historic_yield_multiplier) / self.current_bond_yield
        return round(intrinsic_value, 2)


def main():
    print("-" * 50)
    print("   Benjamin Graham Intrinsic Value Calculator   ")
    print("-" * 50)
    
    try:
        # 1. Gather User Input
        ticker = input("Enter the stock ticker (e.g., NOCIL): ").strip().upper()
        eps = float(input(f"Enter Trailing 12-Month EPS for {ticker}: "))
        growth_rate = float(input("Enter Expected Annual Growth Rate (e.g., for 5%, enter 5): "))
        bond_yield = float(input("Enter Current AAA Corporate Bond Yield (e.g., 7.5): "))
        
        # 2. Instantiate the Object
        calculator = IntrinsicValueCalculator(current_bond_yield=bond_yield)
        
        # 3. Calculate and Output
        value = calculator.calculate_graham_value(eps, growth_rate)
        
        print("\n" + "=" * 30)
        print("       VALUATION RESULTS       ")
        print("=" * 30)
        print(f"Ticker:                    {ticker}")
        print(f"Estimated Intrinsic Value: ₹{value}")
        print("=" * 30 + "\n")
        
    except ValueError:
        # Catches the error if the user inputs a string instead of a float
        print("\n[System Error] Invalid input detected. You must enter numerical values for financial metrics.")

if __name__ == "__main__":
    main()
