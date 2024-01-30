# Lombok

##1. Cleanup annotation
**@Cleanup** can automatically manage various resources that need to be released, such as input and output streams, and ensure that the close method is called safely.

It is used by prefixing the declared resource with @Cleanup, for example:
```
public class fileUtil {
    public InputStream openFile(final String name) throws IOException {
        @Cleanup InputStream in = new FileInputStream("some/file");
        return in;
    }
}
```
Let’s see what the .class file looks like after compiling:
```
public class fileUtil {
    public InputStream openFile(final String name) throws IOException {
        InputStream in = new FileInputStream("some/file");
        FileInputStream var3;
        try {
            var3 = in;
        } finally {
            if (Collections.singletonList(in).get(0) != null) {
                in.close();
            }
        }
        return var3;
}
```
This way, when your code finishes executing, Lombok will automatically call the in.close() method in a try-finally block, freeing up resources.


