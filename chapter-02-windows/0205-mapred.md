##  Windows 下编写 Map/Reduce 测试程序-统计最高气温

1. 修改 etc/hadoop/hdfs-site.xml
    ```xml
    <configuration>
        <property>
            <name>dfs.permissions</name>
            <value>false</value>
        </property>
    </configuration>
    ```
2. 以管理员身份打开 Eclipse。

### 创建项目

1. File > New > Ohter...
2. Select a wizard > Map/Reduce Project
    - Next
3. MapReduce Project
    - Project name: temp.max.client
    - \[x] Use default location
    - \[x] Use default Hadoop
    - Next
4. Java Settings
    - Source > temp.max.client/src(new)
    - Default output folder: temp.max.client/bin
    - Finish

### 检查或增加 jar 包

1. Project Exporer > temp.max.client > JRE System Library
2. Project Exporer > temp.max.client > Reference Libraries

### 如果 Hadoop 的 jar 包 没有导入

1. Package Explorer > temp.max.client > 鼠标右键 > Build Path > Configure Build Path...
2. Properties for temp.max.client > Java Build Path > Libraries > Classpath
2. Add Library > User Library
    - Next
3. User Library
    - User Libraries...
4. Preferences > Java > Build Path > User Libraries
    - New...
    - New User Library
        - User library name: hadoop
        - OK
    - Add Extermal JARS...
        - D:/students/20211202/bd1/idea/hadoop-3.3.1/share/hadoop/**/*.jar
    - Apply and Close
5. User Library
    - User libraries: \[x] hadoop
    - Finish

### 编写测试代码

1. Project Explorer > temp.max.client > src > 鼠标右键 > New > Package
2. New Java Package
    - Source folder: temp.max.client/src
    - Name: temp.max
    - Finish
3. Project Explorer > temp.max.client > src > temp.max > 鼠标右键 > New > Class
    - Name: MaxTemperature
    - \[x] public static void main(String[] args)
    - Finish
4. Project Explorer > temp.max.client > src > temp.max > 鼠标右键 > New > Class
    - Name: MaxTemperatureMapper
    - Finish
5. Project Explorer > temp.max.client > src > temp.max > 鼠标右键 > New > Class
    - Name: MaxTemperatureReducer
    - Finish
6. 在 MaxTemperature 中增加如下代码
    ```
        static {
            try {
                System.load("D:/students/202222022222/bd1/idea/hadoop-3.2.2/bin/hadoop.dll");
            } catch (UnsatisfiedLinkError e) {
                System.err.println("Native code library failed to load.\n" + e);
                System.exit(1);
            }
        }
    ```
7. MaxTemperature.java
    ```java {.line-numbers}
    // cc MaxTemperature Application to find the maximum temperature in the weather dataset
    // vv MaxTemperature
    package main.java;

    import org.apache.hadoop.fs.Path;
    import org.apache.hadoop.io.IntWritable;
    import org.apache.hadoop.io.Text;
    import org.apache.hadoop.mapreduce.Job;
    import org.apache.hadoop.mapreduce.lib.input.FileInputFormat;
    import org.apache.hadoop.mapreduce.lib.output.FileOutputFormat;

    public class MaxTemperature {

        public static void main(String[] args) throws Exception {
            if (args.length != 2) {
                System.err.println("Usage: MaxTemperature <input path> <output path>");
                System.exit(-1);
            }
        
            Job job = new Job();
            job.setJarByClass(MaxTemperature.class);
            job.setJobName("Max temperature");

            FileInputFormat.addInputPath(job, new Path(args[0]));
            FileOutputFormat.setOutputPath(job, new Path(args[1]));
        
            job.setMapperClass(MaxTemperatureMapper.class);
            job.setReducerClass(MaxTemperatureReducer.class);

            job.setOutputKeyClass(Text.class);
            job.setOutputValueClass(IntWritable.class);
        
            System.exit(job.waitForCompletion(true) ? 0 : 1);
        }
    }
    // ^^ MaxTemperature
    ```
8. MaxTemperatureMapper.java
    ```java {.line-numbers}
    // cc MaxTemperatureMapper Mapper for maximum temperature example
    // vv MaxTemperatureMapper
    package main.java;

    import java.io.IOException;

    import org.apache.hadoop.io.IntWritable;
    import org.apache.hadoop.io.LongWritable;
    import org.apache.hadoop.io.Text;
    import org.apache.hadoop.mapreduce.Mapper;

    public class MaxTemperatureMapper extends Mapper<LongWritable, Text, Text, IntWritable> {

        private static final int MISSING = 9999;
    
        @Override
        public void map(LongWritable key, Text value, Context context) throws IOException, InterruptedException {
            String line = value.toString();
            String year = line.substring(15, 19);
            int airTemperature;
            if (line.charAt(87) == '+') { // parseInt doesn't like leading plus signs
                airTemperature = Integer.parseInt(line.substring(88, 92));
            } else {
                airTemperature = Integer.parseInt(line.substring(87, 92));
            }
            String quality = line.substring(92, 93);
            if (airTemperature != MISSING && quality.matches("[01459]")) {
                context.write(new Text(year), new IntWritable(airTemperature));
            }
        }
    }
    // ^^ MaxTemperatureMapper
    ```
9. MaxTemperatureReducer.java
    ```java {.line-numbers}
    package temp.cluster.max;

    import java.io.IOException;

    import org.apache.hadoop.io.IntWritable;
    import org.apache.hadoop.io.Text;
    import org.apache.hadoop.mapreduce.Reducer;

    public class MaxTemperatureReducer extends Reducer<Text, IntWritable, Text, IntWritable> {
    
        @Override
        public void reduce(Text key, Iterable<IntWritable> values, Context context) throws IOException, InterruptedException {
            int maxValue = Integer.MIN_VALUE;
            for (IntWritable value : values) {
            maxValue = Math.max(maxValue, value.get());
            }
            context.write(key, new IntWritable(maxValue));
        }
    }
    ```

### 执行测试程序

1. Project Explorer > temp.max.client > src > temp.max > MaxTemperature.java > 鼠标右键  > Run As > Run on Hadoop
2. Console
    - Usage: MaxTemperature \<input path> \<output path>
3. Project Explorer > temp.max.client > 鼠标右键 > New > Folder
    - Folder name: intput
    - Finish
4.  Project Explorer > temp.max.client > input > 鼠标右键 > New > File
    - File name: temp.txt
    - Finish
5. Project Explorer > temp.max.client > src > temp.max > MaxTemperature.java > 鼠标右键  > Run As > Run Configurations...
6. Run Configurations > Java Application > MaxTemperature
    - Name: MaxTemperature
    - Main
        - Project: temp.max.client
        - Main class: main.max.MaxTemperature
    - Arguments
        - input output
    - Run
7. MapTemperature.java > Run As > Run on Hadoop
8. temp.max.client > F5
9. Project Explorer > temp.max.client > output > part-r-00000
    ```
    1949 111
    1950 22
    ```
