# Enhancement One: Software Design and Engineering

For the first enhancement, I focused on the design and engineering aspects of the project.
I added a logging service to create meaningful output from the console that would allow easier debugging.

## Narrative

Click [here](https://rayjayshark.github.io/Narratives/SoftwareDesignNarrative_JoshuaRay.docx) to access the narrative I created with this enhancement.

## Code

Click [here](https://rayjayshark.github.io/Enhancements/PokerBot_AlgorithmsEnhancement.zip) to find the zip archive of the project after the enhancement.
After being extracted, the project can be openned in an IDE of your choice and compiles.

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
