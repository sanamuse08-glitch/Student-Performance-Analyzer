# Student-Performance-Analyzer
A Python program that analyzes student performance and provides study insights and trends.
# student_performance_tool.py

# Welcome message
print("=== Student Performance Analyzer ===")
print("Enter multiple students' data and get trends and suggestions.\n")

students = []

# 1. Collect multiple students' data
while True:
    name = input("Enter student name (or type 'done' to finish): ")
    if name.lower() == 'done':
        break
    try:
        math = float(input("Math score (0-100): "))
        science = float(input("Science score (0-100): "))
        study_hours = float(input("Weekly study hours: "))
    except ValueError:
        print("Invalid input. Please enter numbers only.")
        continue
    
    average = (math + science) / 2
    students.append({
        "name": name,
        "math": math,
        "science": science,
        "study_hours": study_hours,
        "average": average
    })
    print(f"{name} added!\n")

# 2. Basic Analysis
if not students:
    print("No student data entered. Exiting program.")
    exit()

# Calculate overall class average
overall_avg = sum(s["average"] for s in students) / len(students)
avg_study_hours = sum(s["study_hours"] for s in students) / len(students)

print("\n=== Summary ===")
print(f"Number of students: {len(students)}")
print(f"Overall class average: {overall_avg:.2f}")
print(f"Average study hours per week: {avg_study_hours:.2f}\n")

# 3. Show individual student performance and suggestions
print("=== Student Insights ===")
for s in students:
    print(f"{s['name']}: Average Score = {s['average']:.1f}, Study Hours = {s['study_hours']}")
    if s["average"] >= 90:
        print("  -> Excellent! Keep up the great work!")
    elif s["average"] >= 75:
        print("  -> Good! Small improvements can help reach top scores.")
    else:
        print("  -> Needs improvement. Focus on key subjects and increase study time.")
    
    if s["study_hours"] < avg_study_hours:
        print(f"  -> Suggestion: Try increasing study hours closer to {avg_study_hours:.1f} per week.")
    print("")

# 4. Trend Analysis
high_perf = [s for s in students if s["average"] >= overall_avg and s["study_hours"] >= avg_study_hours]
low_perf = [s for s in students if s["average"] < overall_avg and s["study_hours"] < avg_study_hours]

print("=== Trend Analysis ===")
print(f"Students studying more and scoring above average: {[s['name'] for s in high_perf]}")
print(f"Students studying less and scoring below average: {[s['name'] for s in low_perf]}")

print("\nProgram completed. You can now use these insights to guide study patterns!")
