#Task2

#!/usr/bin/python3
import rospy # Communication
from geometry_msgs.msg import Twist # Message: position, angle etc

def rotate():
    # Starts a new node
    rospy.init_node('robot_cleaner', anonymous=True)
    velocity_publisher = rospy.Publisher('/turtle1/cmd_vel', Twist, queue_size=10)
    vel_msg = Twist()

    #Receiveing the user's input
    print("Let's move the turtle in an outward spiral path.")
    speed = input("Input your speed:") # Say 1
    speed = float(speed)
    distance = int(-1)
    height = int(-1)

    #Checking if the movement is forward or backwards

    vel_msg.linear.x = abs(speed)


    #Since we are moving just in x-axis
    vel_msg.linear.y= 0
    vel_msg.linear.z = 0
    vel_msg.angular.x = 0
    vel_msg.angular.y = 0
    vel_msg.angular.z = 0
    x=5
    for i in range(1):
         
     # Movement forward x-axis

        while int(distance)<=x:
          #Setting the current time for distance calculus
          t0 = rospy.Time.now().to_sec()
          current_distance = 0
          vel_msg.linear.x = abs(speed)
          #Loop to move the turtle in an specified distance
          distance=int(distance)+1
          while(current_distance < int(distance)+1):
            #Publish the velocity
            velocity_publisher.publish(vel_msg)
            #Takes actual time to velocity calculus
            t1=rospy.Time.now().to_sec()
            #Calculates distancePoseStamped
            current_distance= speed*(t1-t0)
          #After the loop, stops the robot
          vel_msg.linear.x = 0
          #Force the robot to stop
          velocity_publisher.publish(vel_msg)
         
    # Movement upward y-axis 

          t2 = rospy.Time.now().to_sec()
          current_height = 0
          vel_msg.linear.y= abs(speed)
          height=int(height)+1
          while(current_height < int(height)+1):
            #Publish the velocity
            velocity_publisher.publish(vel_msg)
            #Takes actual time to velocity calculus
            t3=rospy.Time.now().to_sec()
            #Calculates distancePoseStamped
            current_height= speed*(t3-t2)
          #After the loop, stops the robot
          vel_msg.linear.y = 0
          #Force the robot to stop
          velocity_publisher.publish(vel_msg)
        
     # Movement backward x-axis
         
          #Setting the current time for distance calculus
          t0 = rospy.Time.now().to_sec()
          current_distance = 0
          vel_msg.linear.x = -abs(speed)
          
          #Loop to move the turtle in an specified distance
          while(current_distance < int(distance)+2):
            #Publish the velocity
            velocity_publisher.publish(vel_msg)
            #Takes actual time to velocity calculus
            t1=rospy.Time.now().to_sec()
            #Calculates distancePoseStamped
            current_distance= speed*(t1-t0)
          #After the loop, stops the robot
          vel_msg.linear.x = 0
          #Force the robot to stop
          velocity_publisher.publish(vel_msg)        

    # Movement downward y-axis 

          t6 = rospy.Time.now().to_sec()
          current_height = 0
          vel_msg.linear.y= -abs(speed)

          while(current_height < int(height)+2):
            #Publish the velocity
            velocity_publisher.publish(vel_msg)
            #Takes actual time to velocity calculus
            t7=rospy.Time.now().to_sec()
            #Calculates distancePoseStamped
            current_height= speed*(t7-t6)
          #After the loop, stops the robot
          vel_msg.linear.y = 0
          #Force the robot to stop
          velocity_publisher.publish(vel_msg)
          distance=int(distance)+1
          height=height+1


if __name__ == '__main__':
    try:
      #Testing our function
      rotate()
    except rospy.ROSInterruptException: pass