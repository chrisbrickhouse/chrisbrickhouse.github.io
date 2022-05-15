---
layout: post
title: "A deep dive into a Decemberists song"

date: 2022-05-14
---
I've always enjoyed *The Decemberists* and one of my favorite songs is "Everything I Try to do Nothing Seems to Turn Out Right" from their EP *Billy Liar*. It's a haunting song where the narrator recounts a past relationship which started and ended poorly. Like any song by *The Decemberists* the lyricism is worth its own analysis, but this post looks instead at the musicality. What makes the music so haunting, and why does it pair well with the lyrics at all? I decided to try my hand at music theory and dive into a song I enjoy to see what makes it tick.

<img src="{{site.baseurl}}/assets/Everything_I_try_to_do.png" alt="Musical score for the song Everything I Try to do Nothing Seems to Turn out Right">

Let's start with the chord progression. Based on [a guitar tab I found](https://tabs.ultimate-guitar.com/tab/the-decemberists/everything-i-try-to-do-nothing-seems-to-turn-out-right-chords-3129632) and [a lot of listening](https://www.youtube.com/watch?v=EQvFAJ0nLrE), I was able to piece together the chords:
C C7 C6 F#dim C6 F#dim G G7 Gadd4 Gadd2 G. The 6ths, 7ths, etc are melodic so we can reduce this down to C F#dim C F#dim G (we'll return to the melody later). Given the F#, we seem to be in the key of G making the chord progression: IV -> vii o -> IV -> vii o -> I. This looks like a common tonic->predominant->dominant->tonic progression, but with some noticable differences. Most obviously the initial tonic chord is missing. The song *starts* on the predominant. The harmonic function of the predominant is to bridge from the stability of the tonic to the tension of the dominant, but there is nothing to bridge. This implies a tonic that has yet to be heard, creating a sense that something is missing. The song proceeds to the dominant which creates a sense of tension to be resolved, but in the first instance we return to the predominant; the tension does not get resolved. The predominant again proceeds to the dominant which finally resolves to the tonic. So why does it feel like we didn't go anywhere?
<figure>
<img class="centered" src="{{site.baseurl}}/assets/harmony-function-diagram-major.svg" alt="Diagram of harmonic functions and chord progressions for the major scale.">
<figcaption class="centered">Copyright 2017 Robert Hutchinson. Licensed under the <a href="https://www.gnu.org/licenses/old-licenses/fdl-1.2.en.html">GFDL 1.2</a></figcaption>
</figure>
The melody is where the song gets particularly interesting. I would argue that the song is in a *lydian* scale, but that's not important for our analysis so let's ignore sharps and flats for now. The main melody for the predominant and dominant sections is C B A F E F, and the main melody for the tonic sections  is G F G/D B A G F D C B. In both sections the melody is simply a long slow decline down the scale. If we return to the original chord progression, this helps us understand the variations on the C and G chords. The chords generally remain static with the root played repeatedly across the melody creating a stationary feeling despite the melodic progression. We start on the root (C), descend to the 7th then the 6th. When the melody should hit the 5th, we instead decend to the 4th and change to the F#dim chord which has dominant function. This chord also contains C and so the harmony remains relatively static. Interestingly, the C we get in the F#dim chord is now a 5th rather than the root, so in the context of our walk down the scale, we still get the next degree, a 5th, *but it's the wrong 5th*. The next note in our walk down the scale is E, the 3rd of the root C. This has been part of the C chords being played causing the melody to become ambiguous with the harmony, before going back up to F and transitioning back to an F#dim. This whole time, the harmony has been relatively static, the 1st (C) and 3rd (E) anchoring the melody as it drifts downwards towards them.

<img src="{{site.baseurl}}/assets/Everything_I_try_to_do-melodies.png" alt="Melodies for the song.">

The motif continues in the tonic section with the descent starting on G and some wonkiness as we descend. Like the predominant section, the melody starts on the root of the chord, in this case G. It descends to the 7th with a G7 chord, but then returns to an inverted G chord. This creates an ambiguous melody as the phrase could proceed up to the 1st or down to the 5th. This ambiguity is not resolved as the Gadd4 chord contains both the 3rd (up from the 1st) and the 4th (down from the 5th). The ambiguity continues with the Gadd2 chord as the top part moves down to the added 2nd and the 4th moves down to the third. The top melodic phrase continues down to the root as the bottom melodic phrase remains stationary on the 3rd, resolving both before continuing to the predominant section. These two melodies are interesting when we consider one as a *counter-melody*. Distinct from a harmony, a coutner melody has its own melodic line that stands in a subordinate relationship to the main melody. But which is the main melody and which is the counter? Considering the wider melodic theme of walking down the scale, the bottom line seems to be the main melody as it continues down and resolves on the 3rd like the predominant melody. The counter-melody ascends before descending back to the note where both phrases started.

Throughout the intro and verse we see two ideas: (1) stagnation and (2) messing up. We see stagnation in the chord progression, harmonies, and melodies. Starting with the predominant, we begin in a liminal space between the stability of the tonic and the tension of the dominant. When we finally proceed to the dominant (a transition which breaks the expected melodic progression), we hesitate and return to the predominant before moving forward to the dominant and tonic. The whole time, the harmony is stationary. Through most of the phrase the C and E dyad are played along with every melodic step, and even when we move to the dominant the repetition of the same C holds back the tension. Lastly we see stagnation in the melody and counter-melody. The main melodic theme descends from the root to the 3rd which is also part of the monotonous harmony. The counter-melody in the tonic phrase offers a clearer picture as it ascends from the root only to return, ultiamtely going nowhere as the main melody resolves to the droning 3rd.

The second idea, "messing-up", is more abstract but perhaps the most interesting considering the lyrics. The melodic ideas are simple in concept: step down the scale from 1st to 3rd while playing a C chord then do the same thing for the G chord. The song does not accomplish this melodic feat. The first measure sets up that idea and is accomplished successfully. The second measure however begins with an aborted dominant chord where the 5th is the root of the predominant and the root is the 4th of the predominant. We get our 1, 7, 6, 5, 4 progression, but the 5th and 4th are out of place. It's the *wrong* fifth in the *right* spot and the *right* 4th in the *wrong* spot. Undetered, the song continues to the 3rd in the next chord but in doing so misses the opportunity to resolve the predominant to the tonic. The tonic section continues builds upon this idea by introducing a counter-melody. The coutner-melody is not "messing-up" in itself, but rather represents the narrator messing up their realtionship. What should be a simple descending melody instead splits into two melodic lines, foreshadowing and ultimately mirroring the narrator and their former lover splitting at the end of the song.

But perhaps there is an upside here: viewing these as "mistakes" is only one possible perspective. An important aspect of the lyrics is that the narrator *feels* like nothing turns out right, and it is this anxiety that turns out to be self-fulfilling. The relationship described is not perfect, but there is nothing wrong with it either; it's just fine. The narrator focuses on the aspects that are not perfect and uses this to reinforce their self-conception. When we view the music from this lens, we get a different perspective. The music is not stagnant, but instead has a vibrant melody moving within it. The melodic lines are not mistakes but interesting and complex variations on an otherwise mundane walk down the scale. The narrator's framing restricts our analysis of the music in the same way that it restricts their own analysis of the relationship. To truly appreciate the song, and for the narrator to truly appreciate themself, we need to break out of an analytical frame which focuses only on the "mistakes"; as the card given to the narrator says: "try not to take it so hard."

This song is a wonderful example of how musicality and lyrics can combine to create feelings that could not be conveyed alone, and ultimately yield insight into ourselves and our emotional development. I've always been moved by both the lyrics and music, and while I understood the lyrics rather well, I never sat down and analyzed the music on its own. I haven't done music theory since high school, and I've never analyzed a piece of music at this level of detail before. It was educational, and I learned a lot about music theory. The best part though was just getting to spend some time picking apart one of my favorite songs, even if it didn't turn out right.