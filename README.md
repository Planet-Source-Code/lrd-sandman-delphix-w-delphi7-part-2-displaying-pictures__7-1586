<div align="center">

## DelphiX w\. Delphi7 \- part 2 \- displaying pictures


</div>

### Description

Part 2 of a tutorial on how to make games using DirectX in Delphi.
 
### More Info
 


<span>             |<span>
---                |---
**Submitted On**   |
**By**             |[Lrd\.Sandman](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByAuthor/lrd-sandman.md)
**Level**          |Beginner
**User Rating**    |5.0 (15 globes from 3 users)
**Compatibility**  |Delphi 7
**Category**       |[Games](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByCategory/games__7-38.md)
**World**          |[Delphi](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByWorld/delphi.md)
**Archive File**   |[](https://github.com/Planet-Source-Code/lrd-sandman-delphix-w-delphi7-part-2-displaying-pictures__7-1586/archive/master.zip)





### Source Code

<table border="0" cellpadding="0" cellspacing="0" style="border-collapse: collapse" bordercolor="#111111" width="100%" id="AutoNumber1">
 <tr>
  <td width="100%" align="center"><font size="4">-<b>DelphiX for Delphi7</b></font><p>&nbsp;</td>
 </tr>
 <tr>
  <td width="100%" align="center"><b>Part 2 - </b>Displaying pictures
  <hr></td>
 </tr>
 <tr>
  <td width="100%">Now that we've got our blank project up and running it's
   time to display some pictures and animations.<p>First we'll start by making a simple picture. Start up paint or a
   similar program and create a picture, I used a simple smilie.
   The background is Fucsia, this might look odd, but when you load the image
   you can make one color transparent. So all you have to do is choose a
   color you'll never use and I personally almost never use Fucsia. You could
   choose any color you like, keep in mind that you have to take a color that
   is not in the picture itself (or do if you&nbsp; want part of the picture
   to be transparent).<p>Select the DxImagelList and go to the 'items' option
   (and double-click on the '...' button), a popup will show. Press the 'Add
   New'-button,&nbsp; then go to
   'Picture' in the OI (click the '...') and select the smilie image. The
   'Transparent Color' should set to Fucsia automatically, if it's not then
   set it to Fucsia.<p>We now have a picture ready for use, so let's display
   it on the screen. To do so we'll have to add some code, since this is a
   simple picture we'll just draw it statically with the timer. Go to the
   OnTimer event, it should say something like 'DxDraw1.Flip' depending on
   what you've called it. Add the following code above(!) this line:<p><i>dximagelist1.Items[0].Draw(dxdraw1.Surface, 100, 100, 0);</i><p>This
   draws item 0 of the DxImageList to the surface of DxDraw at position
   100,100 with an index-pattern of 0 (you can forget the index-pattern for
   now).<p>Press F9 and see how the program outputs a smilie on the screen.
   If you're not seeing anything, you've probably forgot to set the DxDraw
   option of your DxImageList to DxDraw1.<br> Eventhough the smilie can't do
   anything, it does mean you know how to display static images on the
   screen.&nbsp;
   <p>You'll probably like to know how you can move this image around, well
   that's pretty simple. Go to Form1 in the OI and double-click 'KeyDown' to
   get to the code-editor. We'll have to set up x and y variables so we can
   set the image inside the timer-loop, but with variables from outside it.
   Insert the following code to the global variable section (under Form1 :
   TForm1):</p>
   <p><i> x_pos : integer;<br>
 y_pos : integer;</i></p>
   <p>Actually a TPoint would be nicer, but that's beyond the scope of this
   tutorial. In addition you'll have to add some code to actually do
   something when u press a direction.</p>
   <p><i>if Key = vk_left then<br>
 x_pos := x_pos - 1;<br>
   <br>
   if Key = vk_right then<br>
 x_pos := x_pos + 1;<br>
   <br>
   if Key = vk_up then<br>
 y_pos := y_pos - 1;<br>
   <br>
   if Key = vk_down then<br>
 y_pos := y_pos + 1;</i></p>
   <p>The Key value holds the Virtual Keycode (vk) of the pressed key, so
   what this does is set the x/y position when pressing one of the 4
   direction keys. The TForm1.FormKeyDown (double-clickon the OnKeyDown
   event&nbsp; in the OI should look like this when you've
   added the code:</p>
   <p>{******************************************************}</p>
   <p><i>procedure TForm1.FormKeyDown(Sender: TObject; var Key: Word;<br>
 Shift: TShiftState);<br>
   begin<br>
   <br>
   if Key = vk_left then<br>
 x_pos := x_pos - 1;<br>
   <br>
   if Key = vk_right then<br>
 x_pos := x_pos + 1;<br>
   <br>
   if Key = vk_up then<br>
 y_pos := y_pos - 1;<br>
   <br>
   if Key = vk_down then<br>
 y_pos := y_pos + 1;<br>
   <br>
   end;</i></p>
   <p>{******************************************************}</p>
   <p>Go to the OnTimer event again and change the line above dxdraw1.flip
   to:</p>
   <p><i>dximagelist1.Items[0].Draw(dxdraw1.Surface, x_pos, y_pos, 0);</i></p>
   <p>Just like the first time, this displays the smilie on DxDraw1, but this
   time at a variable position x_pos, y_pos. In addition we have to set the
   'KeyPreview' option (OI) to 'true' so that the form captures our key
   presses, no matter what component has the focus.<br> Now press F9 to run
   the program, it should run despite the fact that we didn't give x_pos,
   y_pos any starting values. Delphi turns the NULL/nil value to a 0, making
   the starting point at 0,0. Since you'll want to be able to display images
   on a different spot we'll add some more code, this time in the Form1
   OnCreate event (OI). Simply setting the x and y starting values to 150:<p><i>x_pos := 150;<br>
   y_pos := 150;</i><p>That's all, if you run the program again it will start
   at 150,150. It's also the end of this part, one note though; The smilie
   moves quite slow, if you want to speed up the movement change the 'x_pos
   := x_pos + 1' to a higher integer. Same goes for the other 3. Don't worry
   about any weird effects, this is because you're not using a background.
   Head over to the next part to see how to fix that and learn about flickering.<p>Download
   the source-code at darkangeldev.com (articles/tutorials). Any comments or errors are always welcome,
   I hope you enjoyed this tutorial and see you&nbsp; in part 3! </td>
 </tr>
</table>
Go to Devcenter.darkangeldev.com for an outlined tutorial including images..

