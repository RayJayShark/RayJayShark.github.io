# Enhancement One: Software Design and Engineering

For the first enhancement, I focused on the design and engineering aspects of the project.
I added a logging service to create meaningful output from the console that would allow easier debugging.

## Narrative

Click <a href="https://rayjayshark.github.io/Narratives/SoftwareDesignNarrative_JoshuaRay.pdf" target="_blank">here</a> to access the narrative I created with this enhancement.

## Code

Click <a href="https://github.com/RayJayShark/PokerBot/tree/category1-software-design-engineering" target="_blank">here</a> to find the repository for this project.
The link takes you directly to the branch for this enhancement.

### Important Examples

#### LogObject

One important snippit of this enhancement is the LogObject abstract class that is used as a framework for more specific logs.
You can see the imformation that is stored with each log.

```cs
  public abstract class LogObject
  {
      public enum Severity
      {
          Info,
          Warning,
          Error
      }

      public Severity LogSeverity { get; set; }
      public string LogContent { get; set; }
      public Exception? StoredException { get; set; }
  }
```

#### WriteLog()

The WriteLog() method in the LogService class is used to write the log information to the console.

```cs
  public void WriteLog(LogObject log)
  {
      if (log.LogSeverity > _logLevel) return;
      Console.WriteLine(GetTimestamp() + $" - {log.LogSeverity} - {log}");

      if (log.StoredException != null)
      {
          Console.WriteLine("\t" + log.StoredException.StackTrace);
      }
  }
```
