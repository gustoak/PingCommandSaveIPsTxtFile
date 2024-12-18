# Procedure to Execute Ping Command and Save IPs to a Text File

This procedure describes how to use a `for` loop in Windows CMD to execute the `ping` command and save responding IP addresses to a text file.

## Command
```cmd
for /L %i in (0,1,255) do ping -n 1 172.17.0.%i -4 | findstr -m "bytes=32" >> ipaddress.txt
```

## Command Explanation

### General Structure of the Command
The command uses a `for` loop to iterate over a range of values, executing the `ping` command for each value and checking for a response. If a response is received, the IP address is saved to a text file named `ipaddress.txt`.

### Parameters
1. **`for /L`**:
   - Indicates a numerical loop with a defined range.
   - **Syntax**: `for /L %variable in (start,step,end) do command`
     - `start`: Initial value of the loop (in this case, 0).
     - `step`: Increment to be used for each iteration (in this case, 1).
     - `end`: Final value of the loop (in this case, 255).

2. **`%i`**:
   - Variable that holds the current iteration value.
   - In `.bat` scripts, use `%%i` (double percentage signs).

3. **`ping -n 1 172.17.0.%i -4`**:
   - Executes the `ping` command for the IP address `172.17.0.%i`.
     - **`-n 1`**: Sends only 1 packet to the IP address.
     - **`-4`**: Ensures the command uses IPv4.

4. **`| findstr -m "bytes=32"`**:
   - Filters the output of the `ping` command to find lines containing "bytes=32" (indicating a successful response).
   - **`-m`**: Displays only the file name (in this case, the filtered output from `ping`).

5. **`>> ipaddress.txt`**:
   - Redirects the output to the file `ipaddress.txt`.
   - Uses `>>` to append to the file without overwriting existing data.

## Step-by-Step Instructions

1. **Open the Command Prompt (CMD)**:
   - Press `Win + R`, type `cmd`, and press Enter.

2. **Run the Command**:
   - Enter the following command:
     ```cmd
     for /L %i in (0,1,255) do ping -n 1 172.17.0.%i -4 | findstr -m "bytes=32" >> ipaddress.txt
     ```
   - Press Enter.

3. **Check the Results**:
   - After the command completes, open the file `ipaddress.txt` in the same directory where the command was executed.
   - The file will contain the IP addresses that responded to the `ping` command.

4. **Using in Scripts (.bat)**:
   - To use the command in a `.bat` script, replace `%i` with `%%i`:
     ```cmd
     for /L %%i in (0,1,255) do ping -n 1 172.17.0.%%i -4 | findstr -m "bytes=32" >> ipaddress.txt
     ```

5. **Change IP Range (Optional)**:
   - Modify the range `172.17.0.%i` to the desired IP range.

## Example
To check the IP range `192.168.1.x`:
```cmd
for /L %i in (0,1,255) do ping -n 1 192.168.1.%i -4 | findstr -m "bytes=32" >> ipaddress.txt
```

## Notes
- Ensure you have permission to execute the `ping` command and create files in the current directory.
- The file `ipaddress.txt` will be created or updated in the same location where the command is executed.

## License
This document is licensed under the [MIT License](LICENSE).

