# ultrasonic-with-arduino-and-python

from time import sleep
from time import time
from pyfirmata import INPUT, OUTPUT, SERVO
#khai bao thu vien INPUT, OUTPUT, SERVO trong python
from pyfirmata import Arduino, util
#khai bao thu vien Arduino trong python

#install sensor



class Ultrasonic:
    
    def __init__(self): #setup chan arduino
    # ham thuc thi dau tien nhat.
        board = Arduino('COM3')
        sleep(3)

        trig = 8 #chan 8 Arduino phat xung
        echo = 9 #chan 9 Arduino nhan xung
        servo = 10#chan 10 nhan dieu khien servo DC trong cua tu dong
        board.digital[trig].mode = OUTPUT #OUTPUT la chan digital
        board.digital[echo].mode = INPUT#INPUT la chan digital
        
        
    def send_trig_pulse(self):    
    # ham phat mot xung tu chan trig va cach nhau
    # 15ms giua cac lan phat xung.
        Arduino.output(self.trig,True)
        time.sleep(0.00015)
        Arduino.output(self.trig,False)
        
    def wait_for_echo(self,value,timeout):
    # ham chờ xung nhan duoc.
        count = timeout
        while Arduino.input(self.echo) != value and count>0:
            count = count-1
            
    def get_distance(self):
    #def run and get distance
        distance_cm=[0,0,0,0,0]
        for i in range(3):
            self.send_trig_pulse()
            self.wait_for_echo(True,10000)
            start = time.time()
            self.wait_for_echo(False,10000)
            finish = time.time()
            pulse_len = finish-start #elapse time
            distance_cm[i] = pulse_len/0.000058
        distance_cm=sorted(distance_cm)
        return int(distance_cm[2])#tra ve gia tri khoang cach do duoc
    
    def get_speed(self):
         if distance_cm <= 300 and distance_cm >=100:
         #vung khao sat cach cam bien tu 300cm-200cm
            n = len(distance_cm)
            #n la so lan dem thoi gian trong vung khao sat
            speed_value = 2 / n
            #lay quang duong (200cm) chia tong so thoi gian
            #2m = 300cm-100cm
            if speed_value <= 1.4:
            #van toc trung binh nguoi di bo 5km/h = 1,4m/s
                speed_value = low
            elif speed_value > 1.4 and speed_value <= 2.8:
            #van toc trung binh chay bo 10km/h = 2,8m/s
                speed_value = medium
            elif speed_value > 2.8:
                speed_value = fast
            return speed_value
            print(f"van toc hien tai: {speed_value}")
    def run_speed(self):
        if distance_cm < 100 and distance_cm >= 0:
        #vung khoi tao va dieu khien servo quay mo cua
            run.get_pulse_servo(self,pulse)
            print(f"thuc hien mo cua che do: {speed_value}")
            #thuc hien mo cua va dong cua
        elif distance_cm > 300:
        #ngoai vung khao sat
            print("Out of range")
            #thong bao khong tim thay vat the



class Servo:
    def __init__(self):
    #ham thu thi dau tien nhat
        
        servo = 10#chan 10 nhan dieu khien servo DC trong cua tu dong
        board.digital[servo].mode = SERVO#SERVO la chan digital
        servo1 = Arduino.PWM(10,50) #chan 10, 50Hz
        servo1.start(0) #start servo =0
        time.sleep(0.5)#delay 500ms
        
    def get_pulse_servo(self, pulse):
     #ham get and run PWM
        if speed_value.get_speed == low:
            duty = 2 #(180/12)*2=15 do moi buoc
        elif speed_value.get_speed == medium:
            duty = 4#(180/12)*4=60 do moi buoc
        elif speed_value.get_speed == fast:
            duty = 6#(18/12)*6=90 do moi buoc
        return duty #tra ve gia tri duty
        while duty <= 12: #servo = 180 degrees
            servo1.ChangeDutyCycle(duty) #servo thay doi muc
            time.sleep(2) #delay 1s
            duty += duty  #servo tang muc 
        time.sleep(1)#delay 1s
        servo1.ChangeDutyCycle(7)#tro ve 90 do
        time.sleep(0.5)#delay 50ms moi buoc
        servo1.ChangeDutyCycle(2)#tro ve 0 do
        time.sleep(0.5)#delay 500ms moi buoc
        servo1.ChangeDutyCycle(0)# tro ve 
        
#-----END_CODE-----#
   
        

    


    



       
    
        
    
                
                
                
    
    
        

    


    

