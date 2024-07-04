# Function to calculate temperature using quadratic equation
def temperature_model(time, a, b, c):
    starting_temperature = 22.0  # Initial temperature in Celsius
    return starting_temperature + a * time + b * time**2 + c

def read_coefficients_from_file(filename):
    coefficients = {}
    with open(filename, 'r') as file:
        for line in file:
            if line.strip():
                key, value = line.strip().split(' = ')
                coefficients[key.strip()] = float(value)
    return coefficients

def main():
    print("Welcome to the Weather Prediction Program\n")

    # Hard-coded initial values
    hardcoded_a = 0.5
    hardcoded_b = 0.1
    hardcoded_c = 4

    # Menu for options
    print("Select an option:")
    print("1. Use hard-coded initial values")
    print("2. Read coefficients from file")
    print("3. Enter new coefficients via keyboard input")
    print("4. Input multiple sets of coefficients")

    choice = input("Enter your choice (1/2/3/4): ").strip()

    if choice == '1':
        a = hardcoded_a
        b = hardcoded_b
        c = hardcoded_c
        time = float(input("Enter time in hours: "))
        calculate_and_print_temperature(time, a, b, c)

    elif choice == '2':
        filename = 'file.txt'
        file_coefficients = read_coefficients_from_file(filename)
        a = file_coefficients.get('humidity', hardcoded_a)
        b = file_coefficients.get('solar', hardcoded_b)
        c = file_coefficients.get('constant', hardcoded_c)
        time = file_coefficients.get('time', 3)
        calculate_and_print_temperature(time, a, b, c)

    elif choice == '3':
        a = float(input("Enter coefficient 'a' (humidity): "))
        b = float(input("Enter coefficient 'b' (solar intensity): "))
        c = float(input("Enter constant term 'c': "))
        time = float(input("Enter time in hours: "))
        calculate_and_print_temperature(time, a, b, c)

    elif choice == '4':
        multiple_sets = True
        while multiple_sets:
            a = float(input("Enter coefficient 'a' (humidity): "))
            b = float(input("Enter coefficient 'b' (solar intensity): "))
            c = float(input("Enter constant term 'c': "))
            time = float(input("Enter time in hours: "))
            calculate_and_print_temperature(time, a, b, c)

            another_set = input("Do you want to enter another set of coefficients? (y/n): ").strip().lower()
            if another_set != 'y':
                multiple_sets = False

    else:
        print("Invalid choice. Please enter 1, 2, 3, or 4.")
        return

def calculate_and_print_temperature(time, a, b, c):
    temperature = temperature_model(time, a, b, c)
    print(f"At time {time} hours, temperature is {temperature}°C.\n")

if __name__ == "__main__":
    main()
