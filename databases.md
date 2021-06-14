# Enhancement Three: databases

For the third enhancement, I focused on the database aspect of the project.
I added a database table used to store information about the player, such as the amount of money or wins they have.

## Narrative

Click <a href="https://rayjayshark.github.io/Narratives/DatabasesNarrative_JoshuaRay.pdf" target="_blank">here</a> to access the narrative I created with this enhancement.

## Code

Click <a href="https://github.com/RayJayShark/PokerBot/tree/category3-databases" target="_blank">here</a> to find the repository for this project.
The link takes you directly to the branch for this enhancement.

### Important Examples

#### GetPlayerAsync()

This method uses asynchronous operation to access the database and retrieve the data for a player based on their Discord User ID.
I use an ORM called <a href="https://github.com/DapperLib/Dapper" target="_blank">Dapper</a> that allows me to map the data to an object easily.

```cs
  public async Task<PokerPlayer> GetPlayerAsync(ulong id)
  {
      connection.Open();

      try
      {
          return
              await connection.QuerySingleAsync<PokerPlayer>("SELECT * FROM player WHERE discordId = @id",
                  new {id});
      }
      catch (Exception ex)
      {
          Console.WriteLine(ex.Message);
          return null;
      }
      finally
      {
          await connection.CloseAsync();
      }
      
  }
```

