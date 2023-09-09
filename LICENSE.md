import socket

# Function to scan a range of ports on a target host
def scan_ports(target_host, start_port, end_port):
    open_ports = []

    for port in range(start_port, end_port + 1):
        sock = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
        sock.settimeout(1)  # Adjust the timeout as needed
        result = sock.connect_ex((target_host, port))
        
        if result == 0:
            open_ports.append(port)
        
        sock.close()

    return open_ports

if __name__ == "__main__":
    target_host = input("Enter the target host: ")
    start_port = int(input("Enter the start port: "))
    end_port = int(input("Enter the end port: "))

    open_ports = scan_ports(target_host, start_port, end_port)

    if open_ports:
        print(f"Open ports on {target_host}: {', '.join(map(str, open_ports))}")
    else:
        print(f"No open ports found on {target_host}.")
