import datetime

def calculate_bmi(weight, height):
    bmi = weight / (height ** 2)
    return round(bmi, 2)

def assess_heart_risk(age, bmi, systolic_bp, cholesterol):
    risk = 0
    if age > 45:
        risk += 1
    if bmi >= 25:
        risk += 1
    if systolic_bp >= 130:
        risk += 1
    if cholesterol >= 200:
        risk += 1

    if risk == 0:
        return "Low"
    elif risk == 1 or risk == 2:
        return "Moderate"
    else:
        return "High"

def save_report(name, age, bmi, risk_level):
    now = datetime.datetime.now()
    filename = f"{name.replace(' ', '_').lower()}_report.txt"
    with open(filename, "w") as f:
        f.write("==== Health Risk Report ====\n")
        f.write(f"Name         : {name}\n")
        f.write(f"Age          : {age}\n")
        f.write(f"BMI          : {bmi}\n")
        f.write(f"Risk Level   : {risk_level}\n")
        f.write(f"Report Date  : {now.strftime('%Y-%m-%d %H:%M:%S')}\n")
    print(f"📄 Report saved as: {filename}")

def main():
    print("🏥 Welcome to the Health Risk Checker\n")

    name = input("Enter your name: ")
    try:
        age = int(input("Enter your age: "))
        weight = float(input("Enter your weight in kg: "))
        height = float(input("Enter your height in meters (e.g., 1.75): "))
        systolic_bp = int(input("Enter your systolic BP (e.g., 120): "))
        cholesterol = int(input("Enter your cholesterol level (e.g., 180): "))
    except ValueError:
        print("❗ Invalid input. Please enter numbers where required.")
        return

    bmi = calculate_bmi(weight, height)
    risk = assess_heart_risk(age, bmi, systolic_bp, cholesterol)

    print("\n=== Result ===")
    print(f"BMI          : {bmi}")
    print(f"Risk Level   : {risk}")

    save_report(name, age, bmi, risk)

if __name__ == "__main__":
    main()
