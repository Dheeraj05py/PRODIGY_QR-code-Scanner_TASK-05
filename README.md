# PRODIGY_QR-code-Scanner_TASK-05
The Task is here to perform to make a QR Code Scanner app via Python langage.
import cv2
from pyzbar.pyzbar import decode
import webbrowser

# Start camera
cap = cv2.VideoCapture(0)

print("QR Code Scanner Started. Press 'q' to quit.")

while True:
    ret, frame = cap.read()

    # Detect QR codes
    for qr in decode(frame):
        data = qr.data.decode('utf-8')

        # Display scanned text
        print("Scanned Data:", data)

        # Draw rectangle around QR code
        x, y, w, h = qr.rect
        cv2.rectangle(frame, (x, y), (x+w, y+h), (0, 255, 0), 2)

        # If it's a link, open in browser
        if data.startswith("http"):
            print("Opening link...")
            webbrowser.open(data)

    cv2.imshow("QR Code Scanner", frame)

    # Press q to exit
    if cv2.waitKey(1) & 0xFF == ord('q'):
        break

cap.release()
cv2.destroyAllWindows()[QR Code Scanner.py](https://github.com/user-attachments/files/26697279/QR.Code.Scanner.py)
