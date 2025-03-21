Experiment- 
Write shell scripts to print system information.
Write shell script to perform basic mathematical calculation.
Use redirection operators to store the output of commands.

Code- 
//bash//
nano system_info.sh 

//system_info.sh//
OUTPUT_FILE="system_info.txt"

echo "System Information" > $OUTPUT_FILE
echo "==================" >> $OUTPUT_FILE
echo "Hostname: $(hostname)" >> $OUTPUT_FILE
echo "OS Version: $(cat /etc/os-release | grep PRETTY_NAME | cut -d '=' -f2 | tr -d '\"')" >> $OUTPUT_FILE
echo "Kernel Version: $(uname -r)" >> $OUTPUT_FILE
echo "System Uptime: $(uptime -p)" >> $OUTPUT_FILE
echo "Memory Usage:" >> $OUTPUT_FILE
free -h >> $OUTPUT_FILE
echo "Disk Usage:" >> $OUTPUT_FILE
df -h >> $OUTPUT_FILE

cat $OUTPUT_FILE


//bash//
nano math_calc.sh


//math_calc.sh//
OUTPUT_FILE="math_results.txt

echo "Enter first number: "
read num1
echo "Enter second number: "
read num2

echo "Mathematical Calculations" > $OUTPUT_FILE
echo "=========================" >> $OUTPUT_FILE
echo "Addition: $num1 + $num2 = $(expr $num1 + $num2)" >> $OUTPUT_FILE
echo "Subtraction: $num1 - $num2 = $(expr $num1 - $num2)" >> $OUTPUT_FILE
echo "Multiplication: $num1 * $num2 = $(expr $num1 \* $num2)" >> $OUTPUT_FILE
echo "Division: $num1 / $num2 = $(echo "scale=2; $num1 / $num2" | bc)" >> $OUTPUT_FILE

cat $OUTPUT_FILE

//bash//
nano redirection_demo.sh


//redirection_demo.sh//
OUTPUT_FILE="output.txt"
ERROR_FILE="error.txt"

$OUTPUT_FILE
$ERROR_FILE

echo "Listing files in current directory:" > $OUTPUT_FILE
ls >> $OUTPUT_FILE

echo "Trying to list a non-existing directory (error redirected):" >> $OUTPUT_FILE
ls /non_existent_directory 2>> $ERROR_FILE

echo "Checking system uptime and redirecting both stdout & stderr:" >> $OUTPUT_FILE
uptime &>> $OUTPUT_FILE

cat $OUTPUT_FILE
echo "Errors (if any) are stored in $ERROR_FILE."


//bash//
chmod +x system_info.sh math_calc.sh redirection_demo.sh

./system_info.sh

./math_calc.sh

./redirection_demo.sh

cat output.txt
cat error.txt
