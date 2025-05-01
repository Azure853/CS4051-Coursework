# CS4051 Coursework: Student Marks Calculator
# Purpose of the program: Data analytics for student marks
# Developed by Daniel O'Sullivan
# Date Programmed: 21st April 2025

# Helper method to be used when entering student marks
def is_number(s):
    try: # Exception handling
        float(s)
        return True
    except ValueError:
        return False

def get_marks_from_file(): # Enter marks from a file
    file_path = input("Enter the path to the marks file: ") # Ask the user to input the file
    try:
        with open(file_path, 'r') as file:
            data = file.read().splitlines() # Read each line of the file into a list
            marks = []
            for line in data:
                marks.extend([float(x.strip()) for x in line.split(',') if is_number(x.strip())])
                # Use the helper method to validate and parse comma-separated values
            return marks
    except FileNotFoundError: # If the file is not found
        print("The file was not found.")
        return []

def get_marks():
    marks = [] # Initialize marks to an empty list
    while True: # Use a while loop because we want the program to run until a condition is met.
        user_input = input("Enter a student's mark or type 'done' to finish: ") # use 'input' as we want user input
        # Ask the user to enter marks or type 'done' to finish
        if user_input.lower() == 'done':
            break # End the loop if 'done' is entered
        if ',' in user_input: # Allow comme-separated values to be entered
            marks += [float(x.strip()) for x in user_input.split(',') if is_number(x.strip())]
        else: # Add marks one by one
            try:
               mark = float(user_input) # Convert what is entered to a float
               marks.append(mark) # Add the float to the list of marks
            except ValueError: # Check that a number was entered
                print("Please enter a valid number.")
    return marks

def print_menu(marks): # Print the menu for the user
    print("\nYou have entered " + str(len(marks)) + " marks." )
    print("\nMenu:")
    print("1. Print the mean of the numbers")
    print("2. Print the median of the numbers")
    print("3. Print the mode of the numbers")
    print("4. Enter a new set of numbers (replaces existing)")
    print("5. Exit the application")
    print("6. Print the skewness of the numbers")
    print("7. Add more numbers to the current list")

def calculate_mean(marks): # Calculate the mean
    return sum(marks) / len(marks) # Mean is the sum of the data points divided by the number of data points

def calculate_median(marks): # Calculate the median
    sorted_marks = sorted(marks) # Sort the marks
    n = len(sorted_marks) # How many marks are there
    if n % 2 == 1: # If there is an odd number of marks:
        return sorted_marks[ n // 2] # Return mark closest to the middle using floor division.
        # The list is zero-indexed, so we use floor division to round down to the middle index.
    else: # If there is an even number of marks:
        return (sorted_marks[n // 2 - 1] + sorted_marks[n // 2]) / 2 # Returns the average of the two middle indexes.
        # The list is zero-indexed. [n // 2] will give an index just after the middle of the sorted list,
        # whereas [n // 2 - 1] will give an index just before the middle of the sorted list.

def calculate_mode(marks): # Calculate the mode
    frequency = {} # Initialise an empty dictionary
    for mark in marks: # For every mark entered:
        if mark in frequency: # If that mark is in the dictionary
            frequency[mark] += 1 # Add 1 to the dictionary
        else:
            frequency[mark] = 1 # If wasn't in the dictionary, it is now with a value of 1.

    max_freq = max(frequency.values()) # Create a holder for the dictionary item with the highest frequency.
    modes = [] # Initialise an empty list to hold the modes.
    for k, v in frequency.items(): # Loop through all key-value pairs.
        if v == max_freq: # If an data value occurs as many times as the maximum frequency:
            modes.append(k) # Add the data value to the list of modes


    if len(modes) == 1: # If there is a unique mode:
        return modes[0] # Return that mode: the first item on the list of modes.
    else: # If there is not a unique mode:
        return "No unique mode found" # Give a message that no unique mode was found

def calculate_standard_deviation(marks): # Function to calculate standard deviation
    mean = calculate_mean(marks) # Use previously defined function to calculate mean
    n = len(marks) # create a holder for number of marks entered; number of data points.
    variance = sum((x - mean) ** 2 for x in marks) / n # Sum of squares of each data point's distance to the mean
    # divided by number of data points
    return variance ** 0.5 # Return square root of what was calculated.

def calculate_skewness(marks): # Calculate the skewness
    if len(marks) < 3: # Give a message if there are fewer than 3 data points (marks entered)
        return "Skewness requires at least 3 data points"
    mean = calculate_mean(marks) # Use previously defined function to find mean
    median = calculate_median(marks) # Use previously defined function for median
    std_dev = calculate_standard_deviation(marks) # Use previously defined function to find standard deviation
    if std_dev == 0: # Give a message for if the standard deviation is 0
        return "Skewness is undefined when standard deviation is 0"
    n = len(marks) # Holder for number of marks entered
    skewness = 3 * (mean - median) / std_dev # Calculate the skewness using the formula given on Weblearn.
    return skewness


def main():
    marks = []
    while True: # Start by asking the user how they want to enter marks; manual input or read from file
        print("\nHow would you like to enter marks?")
        print("1. Enter marks manually")
        print("2. Read marks from a file")
        print("3. Exit the application")
        choice = input("Enter 1, 2, or 3: ")
        if choice == '1':
            marks = get_marks()
        elif choice == '2':
            marks = get_marks_from_file()
            if marks:
                print(f"Successfully loaded {len(marks)} marks from file.")
        elif choice == '3':
            print("Exiting the application")
            return

        if len(marks) < 2:
            print("Please enter at least two marks.")
            continue

        while True:
            print_menu(marks) # Show the menu after marks have been input
            choice = input("Choose an option: ") # Ask for user input

            if choice == '1': # If 1 is entered
                mean = calculate_mean(marks) # Use the previously defined function to calculate the mean.
                print(f"The mean of the marks is: {mean:.2f}") # Give the mean to two decimal places using an f-string
            elif choice == '2': # If 2 is entered: calculate median
                median = calculate_median(marks) # Use the previously defined function to calculate the median.
                print(f"The median of the marks is: {median}")
            elif choice == '3': # If 3 is entered: calculate mode
                mode = calculate_mode(marks) # Use the previously defined function to calculate the mode.
                print(f"The mode of the marks is: {mode}")
            elif choice == '4': # If 4 is entered: enter a new set of marks
                break # break terminates the inner loop, returning the program to the beginning since the outer
                # while loop is still active.
            elif choice == '5': # If 5 is entered exit
                print("Exiting the application")
                return # The return statement ends the function.
            elif choice == '6': # If 6 is entered: calculate skewness
                skewness = calculate_skewness(marks) # Calculate skewness using previously defined method.
                print(f"The skewness of the marks is: {skewness:.2f}") # print the skewness to two decimal places using
                # an f-string.
            elif choice == '7': # If 7 is entered: add more marks
                more = get_marks() # re-run the get_marks() function.
                marks += more # add the results of the function to the list of marks
            else:
                print("Invalid choice. Please try again.")
                # Exception handling for if none of the given options are chosen.

if __name__ == "__main__":
    main()
