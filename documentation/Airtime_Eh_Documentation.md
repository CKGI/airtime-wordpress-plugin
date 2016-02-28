**Author:** Benjamin Finn &lt;benjaminzfinn@gmail.com&gt;

**Created:** August 17<sup>th</sup>, 2015

**Last Revision:** February 12<sup>th</sup>, 2015

1: Introduction
===============

This document provides an overview and reference source for the functionality of the *Airtime\_Eh* changes to SourceFabric's *Airtime*.

The purpose of the *Airtime\_Eh* project was threefold:

1.  **CRTC Metadata:** To provide a metadata field to allow for the entry of CRTC content category numbers in the existing Airtime metadata fields. This will allow Canadian radio stations an easier time adhering to CRTC guidelines.

2.  **Compendium Management:** As many stations receive their shows in a single compendium file containing many songs, *Airtime\_Eh* provides:

    1.  a way to mark the beginnings and end cues of individual tracks within the compilation

    2.  a way to add metadata fields for each track within the compilation

    3.  a way to playback the compilation as a show consisting of many tracks

3.  **Wordpress Integration of Show History:** As many sites may wish to access the history of shows played by one or more stations, and Wordpress is the most common content management system extant, *Airtime\_Eh* provides a Wordpress plugin which can be used to access a public feed of show histories.

2: Installation
===============

At this time, the *Airtime\_Eh* installation package and Wordpress plugin are available via CKGI's GitHub as installable zip files. It is our hope that our changes will be accepted by SourceFabric and integrated into the usual release of Airtime.

2.1: Installing *Airtime\_Eh*
-----------------------------

To install *Airtime\_Eh*, simply download the package (https://github.com/CKGI/airtime/archive/2.5.x.zip), unzip it anywhere on your system, drop to a terminal, navigate to the directory where you unzipped *Airtime\_Eh*, and then type:

*sudo ./install.sh*

You will then be in an interactive installation mode. Any installation issues you may encounter should be debugged using SourceFabric's usual documentation -- none of the *Airtime\_Eh* modifications will have any impact on installation.

2.2: Installing *Airtime\_Eh* Wordpress Plugin
----------------------------------------------

To install *Airtime\_Eh's* Wordpress plugin, download this package (https://github.com/CKGI/airtime-wordpress-plugin/archive/master.zip). Login as an administrator to your Wordpress site. Go to *Plugins*. On the screen that brings up, click on the *Upload Plugin* link, and follow the instructions.

Once it is uploaded, you may activate the plugin. See Section 4, “Configuring Wordpress," for more information on configuring the plug post-activation.

3: Using *Airtime\_Eh*
======================

*Airtime\_Eh* is, in most ways, a typical Airtime installation. Airtime can be used normally, in accordance to SourceFabric's documentation. However, there are additional features provided by *Airtime\_Eh* which are detailed below.

3.1: CRTC Metadata
------------------

Entering CRTC content category numbers is quite simple. Airtime provides the ability to edit track metadata in the *Library* section of Airtime. To access it, login to your *Airtime\_Eh* installation, go to the *Library* pane pictured below.

<img src="https://raw.githubusercontent.com/CKGI/airtime-wordpress-plugin/master/documentation/media/image1.jpg" width="624" height="479" />

Next, left click on the track whose metadata you wish to edit. A menu will come up. Click on *Edit Metadata*.

<img src="https://raw.githubusercontent.com/CKGI/airtime-wordpress-plugin/master/documentation/media/image2.jpg" width="624" height="479" />

In the fields which come up, the last will read *CRTC*. In that field, enter the CRTC content category or categories of the track, in accordance with CRTC regulations (http://www.crtc.gc.ca/eng/archive/2000/PB2000-14.htm).

Multiple content categories should be entered with a space between them, e.g. 1 11 13.

<img src="https://raw.githubusercontent.com/CKGI/airtime-wordpress-plugin/master/documentation/media/image3.jpg" width="624" height="479" />

When you have entered the content categories, simply click the *Save* button, and the content categories will be stored.

3.2: Configuring *Airtime\_Eh's* Show History Feed
--------------------------------------------------

This is referring to the Airtime side of the equation. To learn more about configuring the Wordpress side, see Section 4, below. This section discusses enabling the show history feed which is consumed by our Wordpress plugin.

Airtime provides the ability for stations to deliver publicly accessible feeds of information relating to their content and status. These feeds are delivered as JSON documents -- bits of text designed to be consumed by other applications in the Javascript Object Notation format, aka JSON.

Please note that although *Airtime\_Eh* only provides a Wordpress plugin to interpret the show history feed, this data can be interpreted in applications by any competent programmer.

*Airtime\_Eh* integrates a show history feed into the pre-existing publicly accessible feeds already provided by Airtime. As such, the show history feed is enabled exactly like the other publicly accessible feeds. For more information on the usual information provided by Airtime's public feeds, see here: http://sourcefabric.booktype.pro/airtime-25-for-broadcasters/exporting-the-schedule/

To enable the show history feed, login to your *Airtime\_Eh* installation. Go to *Preferences*.

<img src="https://raw.githubusercontent.com/CKGI/airtime-wordpress-plugin/master/documentation/media/image4.jpg" width="624" height="479" />

In *Preferences*, go to *Public Airtime API*. Click on *Enabled*. Then go to the bottom of the screen and click *Save.*

<img src="https://raw.githubusercontent.com/CKGI/airtime-wordpress-plugin/master/documentation/media/image5.jpg" width="624" height="479" />

Click *Save*. Now your station provides the usual gamut of publicly available Airtime feeds, including the show history feed.

The show history feed is accessed from a link like this, where you'd replace *www.yourairtimeinstallation.com* with the address of the *Airtime\_Eh* installation whose feed you wish to access:

http://www.yourairtimeinstallation.com/api/showhistory

You may add a configuration variable to that link, like so:

http://www.yourairtimeinstallation.com/api/showhistory?shows=65

This will determine the numbers of shows whose metadata will be delivered. The default is 20 shows; the maximum is 365. This link is what will be entered into your Wordpress plugin's configuration later on, so it's important to note it.

The metadata returned will include the host of the show; the URL of the show; the genre of the show; the description of the show; and a detailed listing of each track played, including starting and ending time of the track, track title, album name, artist name, genre, year of publication, and the track number of the track on its album.

Please note that some of these fields are optional. The only data guaranteed to be received is the host; each track's starting and time; and a track title.

3.3: Using *Airtime\_Eh's* Compendium Functionality
---------------------------------------------------

*Airtime\_Eh* adds a new feature to the editing fields in Airtime's *Library* section, titled *Create Compendium*.

<img src="https://raw.githubusercontent.com/CKGI/airtime-wordpress-plugin/master/documentation/media/image6.jpg" width="624" height="479" />

A compendium file is one where several tracks have been provided to your station as one single file. The purpose of *Create Compendium* is to set **cue points** in the metadata, so Airtime treats each cue point as the beginning and end of a given track. A cue point is simply a timestamp of the beginning and end of a track.

When you click *Create Compendium*, a window will pop up.

<img src="https://raw.githubusercontent.com/CKGI/airtime-wordpress-plugin/master/documentation/media/image7.jpg" width="624" height="479" />

In this window, you will see *Track 1*, and the buttons *Add Track* and *Save Compendium*. *Track 1* has a clickable title. Click it to show or hide the metadata fields for that entry.

<img src="https://raw.githubusercontent.com/CKGI/airtime-wordpress-plugin/master/documentation/media/image8.jpg" width="624" height="479" />

As you can see, each track has the usual metadata fields, but also has a *Starts* and *Ends* field, which represent the starting and ending cue points for this track. These fields expect a numeric entry, in the form of Minute.Seconds (e.g. *3.04* would be three minutes and four seconds). It is important to enter two digits in the second part of the field. If you entered *3.4*, for example, you would be telling the compendium to set a cue point at three minutes and forty seconds, not three minutes and four seconds.

To add further tracks in the compendium, simply click on *Add Track*. Another track entry will appear.

<img src="https://raw.githubusercontent.com/CKGI/airtime-wordpress-plugin/master/documentation/media/image9.jpg" width="624" height="479" />

If you wish to remove a track from the compendium, simply click the *Cancel* button in that track's listing. The offending track will be removed, and the rest will be appropriately re-numbered.

Please note that each track will appear with the metadata revealed for editing. You can click on the title to hide an entry. This will have no effect on the data in that entry, it's simply a convenience for when you have an especially long list of compendium tracks to manage.

When you are finished with your tracks, click *Save Compendium*. The compendium will now appear in your library as a list of tracks which can be sorted into a playlist.

### 3.3.1: Notes on Compendium Usage

Compendiums are an advanced Airtime feature. There are a few tricks to using them properly.

#### 3.3.1.1: Using a Media Player

Airtime's built-in media player is quite limited. As such, it was not feasible to put a media player in the compendium functionality. As such, we advise using a separate media player (i.e. Winamp, VLC, etc.) to find the starting and ending cue points, marking them down, and then entering them into *Airtime\_Eh*.

In addition, when you play the tracks within Airtime, it will not respect the cue points, due to inherent limitations in their built-in media player. To preview a compendium show, you will have to cue it up and play it as a private show.

Simply setup a stream via the Stream settings, and then listen to that stream with the media player of your choice. See the Airtime documentation on setting up multiple streams: http://sourcefabric.booktype.pro/airtime-25-for-broadcasters/stream-settings/

#### 3.3.1.2: Remembering Talking Tracks

Most compendium files delivered will have bits where the content provider (the DJ) is talking. These will have to be marked as well, or they will be omitted when the compendium is saved.

#### 3.3.1.3: Compendiums Are Not Editable

This is important! Once a compendium is saved in Airtime's *Library*, there is no way to edit the cue points. Airtime does not provide that functionality. You need to be sure that the cue points have been set correctly before saving your compendium.

4: Configuring Wordpress
========================

To configure Wordpress for use with our plugin, go into Wordpress' admin screen, and scroll down the side until you see a menu item entitled “Station Feed."

<img src="https://raw.githubusercontent.com/CKGI/airtime-wordpress-plugin/master/documentation/media/image10.jpg" width="624" height="532" />

In *Station Feed*, simply fill in whatever name you'd like to give the station in the *Name* field, and then the URL to the station in the URL field. Please note that this is the URL to the station's Airtime installation, not to their regular website. If in doubt, ask the station what their URL is.

Once you've filled in that information, simply click *Save Station*. The station will now be available as a Wordpress shortcode in the following format: *\[airtime station="Station Name"\]*. You can put this in any post, page, or sidebar, and it will display a feed of the last 20 shows from that station. You may also add a *shows* variable to the shortcode in order to see more or less shows from that station, like so: *\[airtime station="Station Name" shows="65"\]* up to a maximum of 365 shows.

To remove a station, you can either remove the shortcode from your post or page or sidebar, or click *Remove Station* to remove that station from your available list.

In order to add a new station, simply click *Add Station*, and a new set of entry fields will appear, like so:

<img src="https://raw.githubusercontent.com/CKGI/airtime-wordpress-plugin/master/documentation/media/image11.jpg" width="624" height="532" />

Fill in the appropriate details as before, and then you'll have two stations to choose from, and so on.
