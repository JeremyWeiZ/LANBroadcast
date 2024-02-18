# LAN Broadcast in C#
The part of code that handles UDP broadcasting, receiving, and response in C#.
## Key functions
For LAN broadcasting 
```
            UdpClient udpClient = new UdpClient();
            udpClient.EnableBroadcast = true;
            IPEndPoint ip = new IPEndPoint(IPAddress.Broadcast, 12345);
            byte[] bytesToSend = Encoding.ASCII.GetBytes(dangerMessage);
            udpClient.Send(bytesToSend, bytesToSend.Length, ip);
            udpClient.Close();
```
For port listening:
```
            if (listenerThread == null || !listenerThread.IsAlive)
            {
                
                listenerThread = new Thread(() =>
                {
                    UdpClient udpClient = new UdpClient(12345);
                    IPEndPoint remoteEP = new IPEndPoint(IPAddress.Any, 12345);


                    try
                    {
                        
                        while (keepListening)
                        {
                            byte[] bytesReceived = udpClient.Receive(ref remoteEP);
                            string message = Encoding.ASCII.GetString(bytesReceived);
                        }
                    }
                    catch (Exception ex)
                    {
                        // Handle exceptions
                    }
                    finally
                    {
                        udpClient.Close();
                    }
                });

                listenerThread.IsBackground = true;
                listenerThread.Start();

            }
```

