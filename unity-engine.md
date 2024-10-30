# Client integration for unity engine

## step 1
Create a empty object in scene, and rename to "GameManager" <br>
![image](https://github.com/u4hero/client-integration/assets/26012325/383180dc-17a8-49ac-9567-b39a6e84086f)

## step 2
Create a script named "GameManager.cs", and paste the code below:

```
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class GameManager : MonoBehaviour
{
    // Start is called before the first frame update
    void Start()
    {
        // prevent this object to destroy after scene unload
        DontDestroyOnLoad(gameObject);
    }

    // method to pause game (u4play client using this to control)
    public void PauseGame()
    {
        Time.timeScale = 0;
        AudioListener.volume = 0;
    }

    // method to resume game (u4play client using this to control)
    public void ResumeGame()
    {
        Time.timeScale = 1;
        AudioListener.volume = 1;
    }

    // method to mute sound game (u4play client using this to control)
    public void MuteAllSound()
    {
        AudioListener.volume = 0;
    }

    // method to unmute sound game (u4play client using this to control)
    public void UnMuteAllSound()
    {
        AudioListener.volume = 1;
    }

}
```
## step 3
Attach GameManager.cs in GameManager object in scene <br>
![image](https://github.com/u4hero/client-integration/assets/26012325/7587702f-e6ad-4937-b481-4c76dcdab2b9)

## step 4
- Create folder Plugins inside Assets
- Create folder WebGL inside Plugins
- Create file TriggerQuestion.jslib inside WebGL <br>
![image](https://github.com/u4hero/client-integration/assets/26012325/87762e75-daed-41a0-8839-1aba79642f19)
- Open file TriggerQuestion.jslib and paste the code below:
```
mergeInto(LibraryManager.library, {
  TriggerQuestion: function () {
    window.dispatchReactUnityEvent("TriggerQuestion", true);
  },
});
```
This script dispatch events to browser client trigger questions

## step 5
You need to choose what trigger for call questions in your game, we prefer triggers that don't ruin the flow of gameplay, for example:
-  fase end
-  game end
-  game over

## step 6
After choose the trigger, go to script trigger and inser code below:

```
[DllImport("__Internal")]
        private static extern void TriggerQuestion();

        private void RequestQuestion()
        {
   
#if UNITY_WEBGL == true && UNITY_EDITOR == false
	PauseGame();
    TriggerQuestion();
#endif
        }

        public void PauseGame()
        {
            Time.timeScale = 0;
            AudioListener.volume = 0;
        }

        public void ResumeGame()
        {
            Time.timeScale = 1;
            AudioListener.volume = 1;
        }

        public void MuteAllSound()
        {
            AudioListener.volume = 0;
        }

        public void UnMuteAllSound()
        {
            AudioListener.volume = 1;
        }
```
Now you need to call RequestQuestion() method inside your choose trigger.

## step 7
Change build settings for WebGL
![image](https://github.com/u4hero/client-integration/assets/26012325/314bc846-c3ea-43b7-be2c-69bd321b404c)

## step 8
In Player setting change publish settings to

![image](https://github.com/u4hero/client-integration/assets/26012325/eaa7dc4e-7dc4-4619-87ab-714d514eeb43)

Now build the game and upload to U4HERO
