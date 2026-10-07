#  Student Data Entry: Prompt for the number of students
num_students = int(input("Enter the number of students: "))

# Initialize variables to accumulate totals and store student data temporarily
total_grade = 0.0
student_names = []
student_grades = []

# Loop to process each student
for i in range(num_students):
    print(f"\n--- Student {i + 1} ---")
    name = input("Enter student's name: ")

    #  Ensure grade is between 0 and 100 and avoid invalid letters
    while True:
        try:
            grade = float(input("Enter grade (0 - 100): "))
            if 0 <= grade <= 100:
                break
            else:
                print("Invalid grade! Please enter a value between 0 and 100.")
        except ValueError:
            print("Invalid input! Please enter a numerical value.")

    # Store individual records and accumulate total grade
    student_names.append(name)
    student_grades.append(grade)
    total_grade += grade

# Grade Calculation Class total and average
class_average = total_grade / num_students if num_students > 0 else 0.0

# Display Class Statistics
print("\n" + "=" * 40)
print("CLASS SUMMARY")
print("=" * 40)
print(f"Total Class Grade Score: {total_grade:.2f}")
print(f"Class Average Grade:     {class_average:.2f}")
print("-" * 40)

# Display individual student records alongside class average
print(f"{'Student Name':<20} | {'Grade':<10} | {'Class Average':<10}")
print("-" * 40)
for i in range(num_students):
    print(
        f"{student_names[i]:<20} | {student_grades[i]:<10.2f} | {class_average:<10.2f}"
    )
print("=" * 40)



#LISTS AND TUPLES FOR SECTION B

# LIST THE SUJECTS
SUBJECTS = ["AGRICULTURE", "SETSWANA", "MORAL EDUCATION"]

# Multiple Subjects & Data Entry
# Prompt for total number of students
while True:
    try:
        num_students = int(input("Enter number of students: "))
        if num_students > 0:
            break
        print("[!] Please enter a number greater than 0.")
    except ValueError:
        print("[!] Invalid input. Please enter an integer.")

# Master list to store each student as a tuple: (name, [grade1, grade2, grade3])
students = []

for i in range(num_students):
    print(f"\n--- Student {i + 1} Entry ---")
    name = input("Enter student name: ").strip()

    # Store individual student's grades in a list
    grades = []
    for subject in SUBJECTS:
        while True:
            try:
                g = float(input(f"  Enter {subject} grade (0-100): "))
                if 0 <= g <= 100:
                    grades.append(g)
                    break
                print("  [!] Grade must be between 0 and 100.")
            except ValueError:
                print("  [!] Invalid input. Enter a numeric value.")

    # Represent each student as a tuple and add to the list
    student_tuple = (name, grades)
    students.append(student_tuple)

# Enhanced Output & Calculations
# Determine highest and lowest grade for each subject across the entire class
subject_high_low = {}
for idx, subject in enumerate(SUBJECTS):
    subject_grades = [student[1][idx] for student in students]
    subject_high_low[subject] = {
        "highest": max(subject_grades),
        "lowest": min(subject_grades),
    }

# Data Display - Summary Table
print("\n" + "=" * 65)
print("                    STUDENT SUMMARY TABLE")
print("=" * 65)

# Table Header
header = f"{'Student Name':<18} | " + " | ".join([f"{sub:<8}" for sub in SUBJECTS]) + " | {'Average':<8}"
print(header)
print("-" * 65)

# Output each student's name, individual grades, and calculated average
for name, grades_list in students:
    student_avg = sum(grades_list) / len(grades_list)
    grades_str = " | ".join([f"{g:<8.2f}" for g in grades_list])
    print(f"{name:<18} | {grades_str} | {student_avg:<8.2f}")

print("=" * 65)

# Display Highest and Lowest Grade per Subject Across the Class
print("\n" + "=" * 65)
print("            SUBJECT PERFORMANCE (CLASS-WIDE HIGH/LOW)")
print("=" * 65)
print(f"{'Subject':<18} | {'Highest Grade':<18} | {'Lowest Grade':<18}")
print("-" * 65)

for subject in SUBJECTS:
    high = subject_high_low[subject]["highest"]
    low = subject_high_low[subject]["lowest"]
    print(f"{subject:<18} | {high:<18.2f} | {low:<18.2f}")

print("=" * 65)
