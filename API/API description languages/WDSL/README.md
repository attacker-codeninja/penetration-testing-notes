
## `WSDL:Web Services Description Language` is an XML-based language that is used to describe the functionality offered by a web service

## WDSL can be used for SOAP or REST APIs but is more associated with XML Based APIs

## This Videos explain `WDSL` very well
- [explain WDSL in Arabic](https://youtu.be/Xm9cN1dQ3Cg)
- [explain WDSL in English](https://youtu.be/E76xW1JTVXY)


## I will use this example to explain `WDSL` 

```xml
<?xml version="1.0" encoding="UTF-8"?>
<wsdl:definitions targetNamespace="http://tempuri.org/"
	xmlns:s="http://www.w3.org/2001/XMLSchema"
	xmlns:soap12="http://schemas.xmlsoap.org/wsdl/soap12/"
	xmlns:http="http://schemas.xmlsoap.org/wsdl/http/"
	xmlns:mime="http://schemas.xmlsoap.org/wsdl/mime/"
	xmlns:tns="http://tempuri.org/"
	xmlns:soap="http://schemas.xmlsoap.org/wsdl/soap/"
	xmlns:tm="http://microsoft.com/wsdl/mime/textMatching/"
	xmlns:soapenc="http://schemas.xmlsoap.org/soap/encoding/"
	xmlns:wsdl="http://schemas.xmlsoap.org/wsdl/">



<wsdl:types>
		<s:schema elementFormDefault="qualified" targetNamespace="http://tempuri.org/">
			<s:element name="LoginRequest">
				<s:complexType>
					<s:sequence>
						<s:element minOccurs="1" maxOccurs="1" name="username" type="s:string"/>
						<s:element minOccurs="1" maxOccurs="1" name="password" type="s:string"/>
					</s:sequence>
				</s:complexType>
			</s:element>
			<s:element name="LoginResponse">
				<s:complexType>
					<s:sequence>
						<s:element minOccurs="1" maxOccurs="unbounded" name="result" type="s:string"/>
					</s:sequence>
				</s:complexType>
			</s:element>
			<s:element name="ExecuteCommandRequest">
				<s:complexType>
					<s:sequence>
						<s:element minOccurs="1" maxOccurs="1" name="cmd" type="s:string"/>
					</s:sequence>
				</s:complexType>
			</s:element>
			<s:element name="ExecuteCommandResponse">
				<s:complexType>
					<s:sequence>
						<s:element minOccurs="1" maxOccurs="unbounded" name="result" type="s:string"/>
					</s:sequence>
				</s:complexType>
			</s:element>
		</s:schema>


</wsdl:types>




	<!-- Login Messages -->
	<wsdl:message name="LoginSoapIn">
		<wsdl:part name="parameters" element="tns:LoginRequest"/>
	</wsdl:message>
	<wsdl:message name="LoginSoapOut">
		<wsdl:part name="parameters" element="tns:LoginResponse"/>
	</wsdl:message>
	<!-- ExecuteCommand Messages -->
	<wsdl:message name="ExecuteCommandSoapIn">
		<wsdl:part name="parameters" element="tns:ExecuteCommandRequest"/>
	</wsdl:message>
	<wsdl:message name="ExecuteCommandSoapOut">
		<wsdl:part name="parameters" element="tns:ExecuteCommandResponse"/>
	</wsdl:message>




	<wsdl:portType name="HacktheBoxSoapPort">
		<!-- Login Operaion | PORT -->
		<wsdl:operation name="Login">
			<wsdl:input message="tns:LoginSoapIn"/>
			<wsdl:output message="tns:LoginSoapOut"/>
		</wsdl:operation>
		<!-- ExecuteCommand Operation | PORT -->
		<wsdl:operation name="ExecuteCommand">
			<wsdl:input message="tns:ExecuteCommandSoapIn"/>
			<wsdl:output message="tns:ExecuteCommandSoapOut"/>
		</wsdl:operation>
	</wsdl:portType>



	<wsdl:binding name="HacktheboxServiceSoapBinding" type="tns:HacktheBoxSoapPort">
		<soap:binding transport="http://schemas.xmlsoap.org/soap/http"/>
		<!-- SOAP Login Action -->
		<wsdl:operation name="Login">
			<soap:operation soapAction="Login" style="document"/>
			<wsdl:input>
				<soap:body use="literal"/>
			</wsdl:input>
			<wsdl:output>
				<soap:body use="literal"/>
			</wsdl:output>
		</wsdl:operation>
		<!-- SOAP ExecuteCommand Action -->
		<wsdl:operation name="ExecuteCommand">
			<soap:operation soapAction="ExecuteCommand" style="document"/>
			<wsdl:input>
				<soap:body use="literal"/>
			</wsdl:input>
			<wsdl:output>
				<soap:body use="literal"/>
			</wsdl:output>
		</wsdl:operation>
	</wsdl:binding>


	<wsdl:service name="HacktheboxService">
		<wsdl:port name="HacktheboxServiceSoapPort" binding="tns:HacktheboxServiceSoapBinding">
			<soap:address location="http://localhost:80/wsdl"/>
		</wsdl:port>
	</wsdl:service>
</wsdl:definitions>
```


##  WSDL  components:

- **Name**: The name attribute provides a unique identifier for the service within the WSDL document.

- **Port**: A port is a specific endpoint within the service. It defines the network address where the service is accessible and the communication protocol to be used, such as SOAP over HTTP or SOAP over SMTP.

- **Binding**: A binding is an association between a specific port and the protocol and data format used for communication. It links the abstract interface of the service to a concrete network protocol.

-  **Operation**: An operation represents an individual functionality or action that the web service offers. Each operation is associated with input and output messages, defining the data that needs to be sent and received.

- **Message**: A message is an abstract definition of the data being exchanged between the client and the server during an operation. It defines the structure of the input and output data using XML.

- **Types**: The types section defines the data types used in the messages, such as complex data structures, simple data types, and enumerations.


## The best way in my opinion to read WDSL is from bottom to top

### service element : 
```xml
<wsdl:service name="HacktheboxService">

<wsdl:port name="HacktheboxServiceSoapPort" binding="tns:HacktheboxServiceSoapBinding">
<soap:address location="http://localhost:80/wsdl"/>
</wsdl:port>

</wsdl:service>
```

- `<wsdl:service>`: Defines a web service with a specific name. It groups related ports (endpoints) together.
- `<wsdl:port>`: Specifies an endpoint (binding) within the service, defining the network address and communication protocol for that endpoint.




### portType element
```xml
	<wsdl:portType name="HacktheBoxSoapPort">
		<!-- Login Operaion | PORT -->
		<wsdl:operation name="Login">
			<wsdl:input message="tns:LoginSoapIn"/>
			<wsdl:output message="tns:LoginSoapOut"/>
		</wsdl:operation>
		<!-- ExecuteCommand Operation | PORT -->
		<wsdl:operation name="ExecuteCommand">
			<wsdl:input message="tns:ExecuteCommandSoapIn"/>
			<wsdl:output message="tns:ExecuteCommandSoapOut"/>
		</wsdl:operation>
	</wsdl:portType>
```
The `<wsdl:portType>` element defines a set of abstract operations (or methods) that a web service provides.

1. `<wsdl:portType name="HacktheBoxSoapPort">`:
    
    - This defines a `<wsdl:portType>` element with the name "HacktheBoxSoapPort." The port type represents a collection of operations provided by the web service.
2. `<wsdl:operation name="Login">`:
    
    - This defines an operation named "Login" within the port type.
    - An operation represents a specific action that clients can perform on the web service.
3. `<wsdl:input message="tns:LoginSoapIn"/>`:
    
    - This element specifies the input message for the "Login" operation. It refers to a message named "LoginSoapIn" defined in message element using the `tns` namespace.
4. `<wsdl:output message="tns:LoginSoapOut"/>`:
    
    - This element specifies the output message for the "Login" operation. It refers to a message named "LoginSoapOut" in message element using the `tns` namespace.
5. `<wsdl:operation name="ExecuteCommand">`:
    
    - This defines another operation named "ExecuteCommand" within the port type.
6. `<wsdl:input message="tns:ExecuteCommandSoapIn"/>`:
    
    - This element specifies the input message for the "ExecuteCommand" operation. It refers to a message named "ExecuteCommandSoapIn"  in message element using the `tns` namespace.
7. `<wsdl:output message="tns:ExecuteCommandSoapOut"/>`:

    - This element specifies the output message for the "ExecuteCommand" operation. It refers to a message named "ExecuteCommandSoapOut" in message element  using the `tns` namespace.




### message element
```xml
<!-- Login Messages -->
	<wsdl:message name="LoginSoapIn">
		<wsdl:part name="parameters" element="tns:LoginRequest"/>
	</wsdl:message>
	<wsdl:message name="LoginSoapOut">
		<wsdl:part name="parameters" element="tns:LoginResponse"/>
	</wsdl:message>
	<!-- ExecuteCommand Messages -->
	<wsdl:message name="ExecuteCommandSoapIn">
		<wsdl:part name="parameters" element="tns:ExecuteCommandRequest"/>
	</wsdl:message>
	<wsdl:message name="ExecuteCommandSoapOut">
		<wsdl:part name="parameters" element="tns:ExecuteCommandResponse"/>
	</wsdl:message>
```
`<wsdl:message>` element is used to define the abstract message format for each operation in a web service. These messages specify the structure of the data that will be exchanged between the client and the server during the execution of an operation.

1. `<wsdl:message name="LoginSoapIn">`:
    
    - This defines the input message for the "Login" operation.
    - The `name` attribute specifies a unique name for the message.
    - The `<wsdl:part>` element inside the `<wsdl:message>` element describes the content of the message.
    - In this case, the message has a single part named "parameters," and it references the element "tns:LoginRequest," which is defined in types in the WSDL.
2. `<wsdl:message name="LoginSoapOut">`:
    
    - This defines the output message for the "Login" operation.
    - Like the input message, it has a unique name specified by the `name` attribute.
    - The message contains a single part named "parameters," and it references the element "tns:LoginResponse." which is defined in types
3. `<wsdl:message name="ExecuteCommandSoapIn">`:
    
    - This defines the input message for the "ExecuteCommand" operation.
    - Similar to the previous messages, it has a unique name.
    - The message has a single part named "parameters," and it references the element "tns:ExecuteCommandRequest." which is defined in types
4. `<wsdl:message name="ExecuteCommandSoapOut">`:
    
    - This defines the output message for the "ExecuteCommand" operation.
    - It also has a unique name.
    - The message includes a single part named "parameters," and it references the element "tns:ExecuteCommandResponse." which is defined in types



### types element (actual paramters in request or response)
```xml
<wsdl:types>
		<s:schema elementFormDefault="qualified" targetNamespace="http://tempuri.org/">
			<s:element name="LoginRequest">
				<s:complexType>
					<s:sequence>
						<s:element minOccurs="1" maxOccurs="1" name="username" type="s:string"/>
						<s:element minOccurs="1" maxOccurs="1" name="password" type="s:string"/>
					</s:sequence>
				</s:complexType>
			</s:element>
			<s:element name="LoginResponse">
				<s:complexType>
					<s:sequence>
						<s:element minOccurs="1" maxOccurs="unbounded" name="result" type="s:string"/>
					</s:sequence>
				</s:complexType>
			</s:element>
			<s:element name="ExecuteCommandRequest">
				<s:complexType>
					<s:sequence>
						<s:element minOccurs="1" maxOccurs="1" name="cmd" type="s:string"/>
					</s:sequence>
				</s:complexType>
			</s:element>
			<s:element name="ExecuteCommandResponse">
				<s:complexType>
					<s:sequence>
						<s:element minOccurs="1" maxOccurs="unbounded" name="result" type="s:string"/>
					</s:sequence>
				</s:complexType>
			</s:element>
		</s:schema>


</wsdl:types>
```
`<wsdl:types>` element, which is used to define the data types used in the web service. In this case, the data types are specified using XML Schema (XSD) within the `<s:schema>` element. The types are then used to define the structure of the input and output messages for the operations "Login" and "ExecuteCommand."

- `s:schema elementFormDefault="qualified" targetNamespace="http://tempuri.org/">`:
    
    - This defines an XML Schema (XSD) with the target namespace "[http://tempuri.org/](http://tempuri.org/)". The `elementFormDefault="qualified"` attribute means that elements in this schema are namespace-qualified by default.
- `<s:element name="LoginRequest">`:
    
    - This defines the "LoginRequest" data type. It represents the structure of the input message for the "Login" operation.
    - The `<s:complexType>` element indicates that the data type is a complex type, meaning it can have child elements.
- `<s:element minOccurs="1" maxOccurs="1" name="username" type="s:string"/>`:
    
    - This defines the "username" element within the "LoginRequest" type. It is of type "s:string" (string data type) and is required (`minOccurs="1"`) with a maximum occurrence of 1 (`maxOccurs="1"`).
- `<s:element minOccurs="1" maxOccurs="1" name="password" type="s:string"/>`:
    
    - This defines the "password" element within the "LoginRequest" type. It is also of type "s:string" and required with a maximum occurrence of 1.
- `<s:element name="LoginResponse">`:
    
    - This defines the "LoginResponse" data type. It represents the structure of the output message for the "Login" operation.
    - The type contains a sequence with a single element named "result," which can occur multiple times (`maxOccurs="unbounded"`).
- `<s:element minOccurs="1" maxOccurs="unbounded" name="result" type="s:string"/>`:
    
    - This defines the "result" element within the "LoginResponse" type. It is of type "s:string" and can occur multiple times (`maxOccurs="unbounded"`).
- Similar definitions for "ExecuteCommandRequest" and "ExecuteCommandResponse" data types follow the same pattern, representing the structure of input and output messages for the "ExecuteCommand" operation.



### binding element :
- SOAP binding
```xml
<wsdl:binding name="HacktheboxServiceSoapBinding" type="tns:HacktheBoxSoapPort">
		<soap:binding transport="http://schemas.xmlsoap.org/soap/http"/>
		<!-- SOAP Login Action -->
		<wsdl:operation name="Login">
			<soap:operation soapAction="Login" style="document"/>
			<wsdl:input>
				<soap:body use="literal"/>
			</wsdl:input>
			<wsdl:output>
				<soap:body use="literal"/>
			</wsdl:output>
		</wsdl:operation>
		<!-- SOAP ExecuteCommand Action -->
		<wsdl:operation name="ExecuteCommand">
			<soap:operation soapAction="ExecuteCommand" style="document"/>
			<wsdl:input>
				<soap:body use="literal"/>
			</wsdl:input>
			<wsdl:output>
				<soap:body use="literal"/>
			</wsdl:output>
		</wsdl:operation>
	</wsdl:binding>
```

-  the `<wsdl:binding>` element is used to define the protocol and data format details for a specific port type, which represents an endpoint of the web service. 
- It associates an abstract interface (defined in the `<wsdl:portType>` element) with a concrete network protocol, specifying how the messages should be formatted and transmitted over the network.

#### `<wsdl:binding>` contains the following attributes:

- **name**: A unique name that identifies the binding within the WSDL document.
- **type**: A QName (Qualified Name) that references the abstract interface (port type) defined in the `<wsdl:portType>` element, to which this binding corresponds.

Inside the `<wsdl:binding>` element, you use various child elements to specify the actual communication protocol and message formatting details. The elements you include depend on the chosen binding style, which can be either SOAP or HTTP or other custom protocols.

##### For SOAP bindings, the `<wsdl:binding>` element contains: child elements like `<soap:binding>` and `<wsdl:operation>` elements that define how SOAP messages should be transmitted over a specific transport protocol (e.g., HTTP) and the style (e.g., document or RPC) for each operation.

1. `<soap:binding transport="http://schemas.xmlsoap.org/soap/http"/>`:

    - This line specifies the binding details for the web service using SOAP (Simple Object Access Protocol) as the communication protocol.
    - The `transport` attribute sets the transport protocol to HTTP. It means that the SOAP messages will be transmitted over the HTTP protocol, which is a common way of exchanging SOAP messages.
3. `<wsdl:operation name="Login">`:
    
    - This defines an operation named "Login" within the web service. Operations represent the actions that clients can perform on the service.
3. `<soap:operation soapAction="Login" style="document"/>`:
    
    - The `<soap:operation>` element is nested within the `<wsdl:operation>` element to specify SOAP-specific properties for the "Login" operation.
    - `soapAction` attribute: It indicates the SOAP action associated with this operation. SOAP actions are typically URIs that uniquely identify the purpose of the SOAP message. In this case, the SOAP action is set to "Login."
4. `<wsdl:input>`:
    - This element defines the input message for the "Login" operation, which is the data that the client sends to the server when invoking the operation.
    - `<soap:body use="literal"/>`: The `<soap:body>` element specifies how the input message should be formatted inside the SOAP envelope. The `use="literal"` attribute means that the input message will be expressed directly as a literal XML element within the SOAP body.
5. `<wsdl:output>`:
    - This element defines the output message for the "Login" operation, which is the data that the server sends back to the client after the operation is executed.
    - `<soap:body use="literal"/>`: Similar to the input message, the `<soap:body>` element with `use="literal"` attribute indicates that the output message will be expressed directly as a literal XML element within the SOAP body.



- HTTP binding
```xml
<wsdl:binding name="HacktheboxServiceHTTPBinding" type="tns:HacktheboxServicePortType">
  <http:binding verb="POST"/>
  <wsdl:operation name="SomeOperation">
    <http:operation location="SomeOperation"/>
    <wsdl:input>
      <mime:content type="application/json"/>
    </wsdl:input>
    <wsdl:output>
      <mime:content type="application/json"/>
    </wsdl:output>
  </wsdl:operation>
  <!-- More operations go here -->
</wsdl:binding>

```

For HTTP bindings, the `<wsdl:binding>` element includes `<http:binding>` elements to define the details for the HTTP request and response messages. HTTP bindings are commonly used for RESTful web services.

1. `<wsdl:binding name="HacktheboxServiceHTTPBinding" type="tns:HacktheboxServicePortType">`:
    
    - This defines an HTTP binding named "HacktheboxServiceHTTPBinding" associated with the port type "HacktheboxServicePortType."
2. `<http:binding verb="POST"/>`:
    
    - The `<http:binding>` element specifies the details of the HTTP binding. In this case, it sets the HTTP verb to "POST," indicating that requests should be made using the HTTP POST method.
3. `<wsdl:operation name="SomeOperation">`:
    
    - This defines an operation named "SomeOperation" within the web service.
4. `<http:operation location="SomeOperation"/>`:
    
    - The `<http:operation>` element is nested within the `<wsdl:operation>` element to specify the details of the HTTP operation for the "SomeOperation" operation.
    - The `location` attribute specifies the relative URL path for the "SomeOperation" HTTP request. For example, if the service endpoint is "[http://localhost/service](http://localhost/service)", then invoking "SomeOperation" would use the URL "[http://localhost/service/SomeOperation](http://localhost/service/SomeOperation)".
5. `<wsdl:input>` and `<wsdl:output>`:
    
    - These elements define the input and output messages for the "SomeOperation" operation, respectively.
6. `<mime:content type="application/json"/>`:
    
    - The `<mime:content>` element specifies the content type of the input and output messages. In this case, the content type is set to "application/json," indicating that the messages will be in JSON format.