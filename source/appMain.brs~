Sub Main()
    initTheme()
    showSpringboardScreen()  
End Sub

Sub initTheme()

    app = CreateObject("roAppManager")
    theme = CreateObject("roAssociativeArray")
'this is for SD TV
    theme.OverhangPrimaryLogoOffsetSD_X = "25"
    theme.OverhangPrimaryLogoOffsetSD_Y = "10"
    theme.OverhangSliceSD = "pkg:/images/overhang.png"
    theme.OverhangPrimaryLogoSD  = "pkg:/images/oodles.png"
'this is for HD TV
    theme.OverhangPrimaryLogoOffsetHD_X = "50"
    theme.OverhangPrimaryLogoOffsetHD_Y = "20"
    theme.OverhangSliceHD = "pkg:/images/overhang.png"
    theme.OverhangPrimaryLogoHD  = "pkg:/images/oodles2.png"
'Background color setting
    theme.BackgroundColor="#252727"
    theme.SpringboardTitleText="#FFFFFF"
    app.SetTheme(theme)

End Sub


'*************************************************************
'** 		showSpringboardScreen()
'** This function show the roSpringBoardScreen where we display
'** the Thumbnail,title,description,star rating,HD Icon,etc. 
'*************************************************************

Function showSpringboardScreen()
print "showSpringboardScreen started"
    port = CreateObject("roMessagePort")
    screen = CreateObject("roSpringboardScreen")
    screen.SetMessagePort(port)
    item = {   ContentType:"episode"
		Title:"Small bird dances and sings on branch"
               SDPosterUrl:"file://pkg:/images/Thumbnail_SD.jpg"
               HDPosterUrl:"file://pkg:/images/Thumbnail_HD.jpg"
               Description:"A small colorful bird of unknown species dances and chirps on a branch apparently in some kind of mating call. (Includes audio but there are street traffic sounds mingled with bird tweeting)"
	   }
    screen.AddButton(1,"Play")
    screen.AddButton(2,"Go Back")
    screen.SetStaticRatingEnabled(false)
    screen.SetContent(item)
    screen.Show()
    while true
        msg = wait(0, screen.GetMessagePort())
        if type(msg) = "roSpringboardScreenEvent"
            if msg.isScreenClosed()
                exit while                
            else if msg.isButtonPressed()
                    if msg.GetIndex() = 1
                         displayVideo()
                    else if msg.GetIndex() = 2
                         exit while
                    endif
            endif
        endif
    end while
print "SpringboardScreen ended"
End Function

'*************************************************************
'** 			displayVideo()
'** This function is used to play video
'*************************************************************


Function displayVideo()
print "Displaying video: "
    p = CreateObject("roMessagePort")
    video = CreateObject("roVideoScreen")
    video.setMessagePort(p)
    videoclip = CreateObject("roAssociativeArray")
    videoclip.StreamBitrates = [0]
    videoclip.StreamUrls = ["http://archive.org/download/HdVideo-SmallBirdDancesAndSingsOnBranch/bird.mp4"]
    videoclip.StreamQualities = ["HD"]
    videoclip.StreamFormat = "mp4"
    videoclip.Title = "Small bird dances and sings on branch"
    videoclip.IsHD = True
    video.SetContent(videoclip)
    video.show()
    while true
        msg = wait(0, video.GetMessagePort())
        if type(msg) = "roVideoScreenEvent"
            if msg.isScreenClosed() then
                exit while
            else if msg.isPlaybackPosition() then
		print "You can write playback code here"
            else if msg.isRequestFailed()
                print "Playing video failed"
            endif
        end if
    end while
print "displayVideo ended"
End Function

