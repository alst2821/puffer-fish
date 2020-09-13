===================
 Java serial lines
===================

Last tested around 2014.

To list serial ports::

  import java.util.Enumeration;
  import javax.comm.CommPortIdentifier;
  public class ListPorts {
      public static void main(String[] args) {
          Enumeration<CommPortIdentifier> e =
              CommPortIdentifier.getPortIdentifiers();
          while (e.hasMoreElements()) {
              CommPortIdentifier ident = e.nextElement();
              System.out.println(ident.getName());
              System.out.println(ident.getPortType());
          }
      }
  }

To test ports::
  
  import java.util.Enumeration;
  import javax.comm.SerialPort;
  import javax.comm.CommPortIdentifier;
  import javax.comm.CommPort;
  import java.io.InputStream;
  import java.io.BufferedReader;
  import java.io.InputStreamReader;
  import java.io.IOException;
  import javax.comm.PortInUseException;
  
  public class TestPort {
      public static void main(String[] args) throws IOException,PortInUseException {
          Enumeration<CommPortIdentifier> e =
              CommPortIdentifier.getPortIdentifiers();
          while (e.hasMoreElements()) {
              CommPortIdentifier ident = e.nextElement();
              System.out.println(ident.getName());
              System.out.println(ident.getPortType());
              if (ident.getPortType() == CommPortIdentifier.PORT_SERIAL) {
                  System.out.println(ident.getCurrentOwner());
                  CommPort port = ident.open("TestPort", 1000);
                  SerialPort sport = (SerialPort) port;
                  InputStream is = port.getInputStream();
                  BufferedReader rd = new BufferedReader(new InputStreamReader(is));
                  System.out.println("Testing port " + ident.getName());
                  System.out.println("Carrier Detect is " + sport.isCD());
                  for (int i = 1; i < 4; i++) {
                      System.out.println(rd.readLine());
                  }
              }
          }
  
      }
  }
