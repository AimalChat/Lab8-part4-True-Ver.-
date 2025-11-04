Project: zuul-with-enums-v2
Authors: Michael Kölling and David J. Barnes

This project is part of the material for the book

   Objects First with Java - A Practical Introduction using BlueJ
   Seventh edition
   David J. Barnes and Michael Kölling
   
This project is a simple framework for an adventure game. In this version,
it has a few rooms and the ability for a player to walk between these rooms.
That's all.

To start this application, create an instance of class "Game" and call its
"play" method.

This project was written to illustrate the use of enums to support
language independence of the game logic.

Read chapter 8 of the book to get a detailed description of the project.

38. Review the source code of the zuul-with-enums-v1 project to see how it uses the CommandWord type. 
The classes Command, CommandWords, Game, and Parser have all been adapted from the zuul-better 
version to accommodate this change. Check that the program still works as you would expect. 

38b.

39. Add a look command to the game, that prints the long description of the current room. 

39b.
//in enum class
/**
 * Representations for all the valid command words for the game.
 * 
 * @author  Michael Kölling and David J. Barnes
 * @version 7.0
 */
public enum CommandWord
{
    // A value for each command word, plus one for unrecognized commands.
    GO, QUIT, HELP, UNKNOWN, LOOK,
}

//in command words class
import java.util.HashMap;

/**
 * This class is part of the "World of Zuul" application. 
 * "World of Zuul" is a very simple, text based adventure game.
 * 
 * This class holds an enumeration of all command words known to the game.
 * It is used to recognise commands as they are typed in.
 *
 * @author  Michael Kölling and David J. Barnes
 * @version 7.2
 */

public class CommandWords
{
    // A mapping between a command string and the CommandWord
    // associated with it.
    private HashMap<String, CommandWord> validCommands;

    /**
     * Constructor - initialise the command words.
     */
    public CommandWords()
    {
        validCommands = new HashMap<>();
        validCommands.put("go", CommandWord.GO);
        validCommands.put("help", CommandWord.HELP);
        validCommands.put("?", CommandWord.HELP);
        validCommands.put("quit", CommandWord.QUIT);
        validCommands.put("look", CommandWord.LOOK);
    }
//In the game class
/**
     * Given a command, process (that is: execute) the command.
     * @param command The command to be processed.
     * @return true If the command ends the game, false otherwise.
     */
    private boolean processCommand(Command command) 
    {
        boolean wantToQuit = false;

        CommandWord commandWord = command.getCommandWord();

        switch (commandWord) {
            case UNKNOWN -> System.out.println("I don't know what you mean...");
            case HELP    -> printHelp();
            case GO      -> goRoom(command);
            case QUIT    -> wantToQuit = quit(command);
            case LOOK    -> look();
        }
        return wantToQuit;
    }

    // implementations of user commands:
    
    private void look()
    {
        System.out.println(currentRoom.getLongDescription());
    }

40. “Translate” the game to use different command words for the GO and QUIT commands. These could be
from a real language or just made-up words. Do you only have to edit the CommandWords class to 
make this change work? What is the significance of this? 

40b.YES! This makes it so that localization and translation to other languages is faciliated!

41. Change the word associated with the HELP command and check that it works correctly. After you have 
made your changes, what do you notice about the welcome message that is printed when the game starts?

41b.

42. Change your commands so that typing a question mark displays the help text. (In effect, use “?” as the 
help command.) Test. Then extend the implementation so that both the question mark and the string 
“help” can be used to display the help text. 

42b.It doesnt change to the translated word I gave it, even though I did change the keyword for
the help() method because it is hardcoded into the welcome message.

43. Define your own enumerated type called Direction with values NORTH, SOUTH, EAST, and WEST. 

43b.
/**
 * Enumeration class Directions - Words associated with the cardinal directions
 *
 * @author (Aimal)
 * @version (version number or date here)
 */
public enum Directions
{
    NORTH, SOUTH, EAST, WEST,
}

44. Add your own look command to zuul-with-enums-v2. Do you only need to change the CommandWord 
type? 

44b.Yes, well no. You have to add the look() method to which it points to and add a seperate case
for LOOK.

45. Change the word associated with the help command in CommandWord. Is this change automatically 
reflected in the welcome text when you start the game? Take a look at the printWelcome method in the 
Game class to see how this has been achieved

45b. YES!
