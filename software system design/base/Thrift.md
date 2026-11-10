# $Thrift$

[TOC]

# Example

## Server

- 在`pom.xml`中添加下列依赖项

```
    <dependency>
      <groupId>org.apache.thrift</groupId>
      <artifactId>libthrift</artifactId>
      <version>0.12.0</version>
    </dependency>
```



- 定义Thrift接口规范（calculator.thrift）,创建一个名为`calculator.thrift`的文件，并在其中定义我们的计算器服务。

```
namespace java com.example.calculator

service CalculatorService {
  i32 calculate(1:i32 num1, 2:i32 num2, 3:Operation operation)
}

enum Operation {
  ADD,
  SUBTRACT,
  MULTIPLY,
  DIVIDE
}
```

- 使用Thrift编译器生成Java代码：

```shell
thrift -gen java calculator.thrift
```

- 实现服务器端代码

```java
import org.apache.thrift.TException;
import com.example.calculator.*;

public class CalculatorServer implements CalculatorService.Iface {
    @Override
    public int calculate(int num1, int num2, Operation operation) throws TException {
        switch (operation) {
            case ADD:
                return num1 + num2;
            case SUBTRACT:
                return num1 - num2;
            case MULTIPLY:
                return num1 * num2;
            case DIVIDE:
                if (num2 == 0) {
                    throw new InvalidOperation("Cannot divide by zero!");
                }
                return num1 / num2;
            default:
                throw new InvalidOperation("Unknown operation: " + operation);
        }
    }
}

```



## Client

```
import org.apache.thrift.TException;
import org.apache.thrift.protocol.TBinaryProtocol;
import org.apache.thrift.transport.TSocket;
import org.apache.thrift.transport.TTransport;
import com.example.calculator.*;

public class CalculatorClient {
    public static void main(String[] args) {
        try {
            TTransport transport = new TSocket("localhost", 9090);
            transport.open();

            TBinaryProtocol protocol = new TBinaryProtocol(transport);
            CalculatorService.Client client = new CalculatorService.Client(protocol);

            int num1 = 10;
            int num2 = 5;
            Operation operation = Operation.ADD;

            int result = client.calculate(num1, num2, operation);
            System.out.println("Result: " + result);

            transport.close();
        } catch (TException e) {
            e.printStackTrace();
        }
    }
}
```

