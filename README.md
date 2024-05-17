#import the reqired libraries 
import mysql.connector
import pandas as pd
import matplotlib.pyplot as plt

#collect data from the database
timeout = 10
connection = mysql.connector.connect(charset="utf8mb4",
                                      connection_timeout=timeout,
                                      database="defaultdb",
                                      host="mysql-f3601b9-jonesjorney-bd4e.f.aivencloud.com",
                                      password="AVNS_ERXe8j5gIX5yis97hnw",
                                      port=21038,
                                      user="avnadmin")

mycursor = connection.cursor()
mycursor.execute("SELECT Volume, CO2 FROM data")

result = mycursor.fetchall()

# Convert result to DataFrame
df = pd.DataFrame(result, columns=['Volume', 'CO2'])

# Plotting/visualization 
plt.plot(df['Volume'], df['CO2'])
plt.xlabel('Volume')
plt.ylabel('CO2')
plt.title('Volume vs CO2')
plt.ylim(0)  # set minimum y-axis limit to 0
plt.xlim(0)  # set minimum x-axis limit to 0
plt.show()
