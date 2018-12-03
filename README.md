Songplayerino applikatsioon.

# Sisukord
* Tutvustus
  1. Mis on SongPlayerino ning tema eesmärk?
  2. Kellele on see äpp mõeldud?
  3. Kuidas ta toimib?
* Põhjalikumalt äppi funktsioonidest
  1. Funktsioon - laulud
  2. Funktsioon - meedia mängija
     1. Previous
     2. Revert
     3. Pause/Continue
     4. Forward
     5. Next
  3. Funktsioon - lisavalikud
     1. Shuffle Songs
     2. Exit
  4. Funktsioon - taustavalikud
 * Tähtsam koodi ülesehitus, selgitus
     1. XML failid
     2. Klassi failid
 * Tuntumad vead
 * Prototüüp

# Tutvustus

## Mis on SongPlayerino ning tema eesmärk?

SongPlayerino on põhiliselt lihtne Androidi app, mille peamiseks eesmärgiks on muusikat mängida.

## Kellele on see äpp mõeldud?

SongPlayerino on mõeldud kasutajatele, kes soovivad kuulata muusika kiire nupu vajutusega ning kes tahavad, et muusika mängiks automaatselt järjest või suvalises järjekorras.

## Kuidas ta toimib?

Toimib ta nii, et kui kasutaja äppi tööle paneb, siis küsib kasutaja käest luba sinu meedia failide ligi, nagu alltoodud pildil

![PREMISSION PILT](https://puu.sh/yv5Rt/fcbd64cd49.png)

Äppil on vaja luba sinu meedia failidele, sest ainult siis saab ta mängida sulle sinu muusika faile. Kui luba ei anta, ei kuva äppis ühtegi meedia faili ning üldiselt äpp siis ei tööta. Kui anda luba, siis kuvab äpp ette kõik meedia failid, mis ta on sinu telefonist leidnud. Tuleb meelest pidada, et ta võtab ka duplikaadid, kui telefonil neid on.

![MAIN PILT](https://puu.sh/yv5S0/4f2f65a8c4.png)

NB! Nagu eelnevalt öeldud, kuvab äpp ette KÕIK meedia failid, mis tähendab ka seda, et ta võib võtta ka näiteks kas sinu alarmi helitoonid, või mingi teise äppi helid, näiteks Skype Sissetuleva Kõne heli.

# Põhjalikumalt äppi funktsioonidest

## Funktsioon - laulud

Pannes äppi tööle, tulevad sulle ette laulud ja helid nende autoritega. Kui laulul või helil pole autorit, viskab ta autori teksti kohale <unknown>.
Kui sul on palju meediafaile, saab näpuga alla kerides leida veel meediafaile.

## Funktsioon - meedia mängija

Vajutades mingi meediafaile teksti peale, hakkab meediafail mängima, ning alla tekib player, kus on sul on sul mitu valikut ning edenemis riba numberitega, kui pikk maa on laulul läbitud ja kui palju on maksimum, ehk siis kui pikk on meediafail:

![PLAYER PILT](https://puu.sh/yv6ey/333ba5939d.png)

### Previous
Kõige paremal on **"Previous"** nupp. Sellele vajutades hakkab mängima eelmine nimekirjas oleval meediafail ning see mis hetkel mängis enne nupule vajutades, rohkem ei mängi.
( Rida läheb nii, et eelnevad laulud on üleval ja järgmised on allpool )

### Revert
Seejärel tuleb nupp **"Revert"**. Kui sellele vajutada, liigub helifail 5 sekundit tagasi. Kui helifail on kestnud vähem, kui 5 sekundit, siis läheb ta 00:00 peale, ehk siis täiesti algusesse (Nt 00:03 pealt vajutades **'Revert'**, läheb ta 00:00).

### Pause/Continue
Järgmisena on **"Pause/Continue"** nupp. Kui helifail mängib, ning pause nupule vajutades, siis jääb helifail seisma, ehk siis pausile. Kui sellele uuesti vajutada, ehk siis kui helifail on pausitud, hakkab helifail uuesti mängima.
Kui helifail on pausil, on logo paremale nool, kui aga pausilt maha võtta, muutub nupu logo teistpidi võrdusmärgiks.

### Forward
Järgmisena on **"Forward"** nupp. See töötab nagu **'Revert'** nupp, ainukesed 2 muutust on see, et ta lükkab helifaili edasi, mitte tagasi, ning ta lükkab edasi 15 sekundit, mitte 5 sekundit.

### Next
Ja lõpuks on **"Next"** nupp, mis töötab samamoodi nagu **'Previous'** nupp, ainuke vahe on see, et ta võtab nimekirjast järgmise helifaili, mitte eelmise.


## Funktsioon - lisavalikud
Üleval paremal pool on kolm täpikest, nendele vajutades tuleb ette 2 lisavalikut.

![OPTIONAL CHOICES](https://puu.sh/yvalm/9931175393.png)

### Shuffle Songs
Nupp **"Shuffle Songs"** ajab sul helifailid segamini, et ta mitte ei mängi järjest helifaile, vaid võtab suvalisi. Ta ei kordu enne, kui on kõik helifailid läbi käinud suvalisel teekonnal. Sellest saab lahti, kui taaskäivitada oma äpp.

### Exit
Nupp **"Exit"** lihtsalt paneb sul äppi täiesti kinni, muud midagi.

## Funktsioon - taustavalikud
Kui panna helifail mängima, jääb sulla tasuta teade, et sul SongPlayerino äppist mängib helifail. Kui sellele vajutada, viskab see sind äppi kohe tagasi.

![BACKGROUND NOTIFICATION](https://puu.sh/yvaFr/c8c678f9f2.png)

# Tähtsam koodi ülesehitus, selgitus

## XML failid
Tähtsaim asi siin on see, et me lisame ListView, mis hakkab meile näitama meie helifaile.
Muidugi tuleb muuta layout ka LinearLayout-iks, kui juba ei ole.

    <ListView
        android:id="@+id/song_list"
        android:layout_width="wrap_content" 
        android:layout_height="match_parent"         
        android:background="#282828">
    </ListView>

### AndroidManifest.xml
Manifest failis tuleb meile anda õiguesd, et saada ligi telefoni mälule.

    <uses-permission android:name="android.permission.WAKE_LOCK" />
    <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
    <uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE"/>

Siin teeme võimalikuks selle, et kui kasutaja läheb äppist välja, aga ei sulge seda, tekib ülesse teade.

        <activity
            android:name="com.example.j_e.songplayerino.MainActivity"
            android:label="@string/app_name"
            android:launchMode="singleTop"
            android:screenOrientation="portrait" >

### Song.xml
Seejärel tuleb meil luua uus xml fail, kus saame anda kasutajale teate eelmise koodi põhjal, mis heli faili pealkiri on ning tema autor. Layout peab olema jällegi LinearLayout.

    <TextView
        android:id="@+id/song_title"
        android:layout_width="fill_parent"
        android:layout_height="wrap_content"
        android:textColor="#ffd700"
        android:textSize="20sp"
        android:textStyle="bold" />

    <TextView
        android:id="@+id/song_artist"
        android:layout_width="fill_parent"
        android:layout_height="wrap_content"
        android:textColor="#ffef99"
        android:textSize="18sp" />

### Main.xml
Resource(res) kausta tuleb teha uus xml fail. Sinna sisse paneme itemid meediafailide segastamise ja äppi kinni panemiste meetodite jaoks.

    <item
        android:id="@+id/action_shuffle"
        android:icon="@drawable/rand"
        android:orderInCategory="1"
        android:showAsAction="always"
        android:title="Shuffle songs"/>

    <item
        android:id="@+id/action_end"
        android:icon="@drawable/end"
        android:orderInCategory="2"
        android:showAsAction="always"
        android:title="Exit"/>

## Klassi failid

### Song.java
Loome uue klassi nimega Song, kus sees me deklareerime ära meediafaili ID, tiitli e. pealkirja ja autori ning loome meetodid, mis neid tagastavad.

public class Song
{
    private long id;
    private String title;
    private String artist;

    public Song(long songID, String songTitle, String songArtist) {
        id=songID;
        title=songTitle;
        artist=songArtist;
    }

    public long getID(){return id;}
    public String getTitle(){return title;}
    public String getArtist(){return artist;}}

### MusicController.java
Loome veel ühe klassi, kus sees me importime ja otsime välja meedia mängija, mis tekib äppi alla, kui mingi meediafail tööle panna. Õnneks on vajalikud meedia mängija funktsioonid kohe olemas, seega ei pea hakkama ise uusi nuppe ja meetodeid tegema.

`public class MusicController extends MediaController
{
    public MusicController(Context c)`

    {
        super(c);
    }

    public void hide() {}}

### SongAdapter.java
Loome jällegi uue klassi, kus sees me deklareerime kõigepealt ära meediafailide nimekirja, selle layouti XML faili ning otsime need üles.

`public class SongAdapter extends BaseAdapter
{
    private ArrayList<Song> songs;
    private LayoutInflater songInf;`

    public SongAdapter(Context c, ArrayList<Song> theSongs)
    {
        songs=theSongs;
        songInf=LayoutInflater.from(c);
    }

Seega loome Override meetodid, mis võtab meil meediafailide suuruse, võtab eelnevalt loodud itemid ja nende id, ning siis vaate / getView, kus sees me loome mitmeid muutujaid, mis tulevad hiljem kasuks.

    @Override
    public int getCount()
    {
        return songs.size();

    }


    @Override
    public Object getItem(int arg0)
    {
        return null;
    }

    @Override
    public long getItemId(int arg0) {
        return 0;
    }

    @Override
    public View getView(int position, View convertView, ViewGroup parent)
    {
        LinearLayout songLay = (LinearLayout)songInf.inflate(R.layout.song, parent, false);
        TextView songView = (TextView)songLay.findViewById(R.id.song_title);
        TextView artistView = (TextView)songLay.findViewById(R.id.song_artist);
        Song currSong = songs.get(position);
        songView.setText(currSong.getTitle());
        artistView.setText(currSong.getArtist());
        songLay.setTag(position);
        return songLay;
    }}

### MusicService.java
Ning viimaks loome viimase klassi, kus sees hakkab meil muusika teenus tööle.
Kõigepealt loome mõned Listener meetodid.

`public class MusicService extends Service implements
        MediaPlayer.OnPreparedListener, MediaPlayer.OnErrorListener,
        MediaPlayer.OnCompletionListener
{`

Seejärel loome muutujad meediafailide segastamiseks.

    private boolean shuffle=false;
    private Random rand;

Nüüd loome mõned Override meetodid, kõigepealt binderid teiste meetodite abil, et kas panna hetkel mängiv meediafail pausile või jätkata teda pausilt. 

    @Override
    public void onCompletion(MediaPlayer mp)
    {
        if(player.getCurrentPosition()>0)
        {
            mp.reset();
            playNext();
        }
    }

Siis kui tekib mingi viga, taaskäivitame äppi.

    @Override
    public boolean onError(MediaPlayer mp, int what, int extra)
    {
        mp.reset();
        return false;
    }

Nüüd loome muutujad meediafaili pealkirja ja tema ID jaoks. Ning siis loome meetodi, kus paneme hetkese mängiva meediafaili teate äppi taustapildile (ehk siis ülesse), mis ütleb, mis meediafail hetkel mängib.

    private String songTitle="";
    private static final int NOTIFY_ID=1;
    @Override
    public void onPrepared(MediaPlayer mp)
    {
        mp.start();
        Intent notIntent = new Intent(this, MainActivity.class);
        notIntent.addFlags(Intent.FLAG_ACTIVITY_CLEAR_TOP);
        PendingIntent pendInt = PendingIntent.getActivity(this, 0, notIntent, PendingIntent.FLAG_UPDATE_CURRENT);

        Notification.Builder builder = new Notification.Builder(this);

        builder.setContentIntent(pendInt)
                .setSmallIcon(R.drawable.play)
                .setTicker(songTitle)
                .setOngoing(true)
                .setContentTitle("Playing").setContentText(songTitle);
        Notification not = builder.build();

        startForeground(NOTIFY_ID, not);
    }

Loome veel muutujaid meedia mängija jaoks ning meediafailide nimekirja jaoks. Seejärel onCreate meetodi; meetodi mis kutsub meil välja meie eelnevalt deklareeritud Listenerid, mis asuvad teises klassis; listi meetodi, mis paneb meil meediafailid sinna nimekirja; binderi meetodi, kust kutsume MusicService klassi; Loome ka uue binder muutuja; ning seejärel meetodi, kui panna meediafail mängima. See lähtestab meil kõik tagasi normaalolekusse ja paneb meil meediafailid mängima, kui mingit errorit pole.

  `private MediaPlayer player;`

    private ArrayList<Song> songs;

    private int songPosn;

    public void onCreate()
    {
        rand=new Random();

        super.onCreate();

        songPosn=0;

        player = new MediaPlayer();
        initMusicPlayer();
    }

    public void initMusicPlayer()
    {
        //set player properties
        player.setWakeMode(getApplicationContext(), PowerManager.PARTIAL_WAKE_LOCK);
        player.setAudioStreamType(AudioManager.STREAM_MUSIC);

        player.setOnPreparedListener(this);
        player.setOnCompletionListener(this);
        player.setOnErrorListener(this);
    }

    public void setList(ArrayList<Song> theSongs)
    {
        songs=theSongs;
    }

    public class MusicBinder extends Binder
    {
        MusicService getService()
        {
            return MusicService.this;
        }
    }
    private final IBinder musicBind = new MusicBinder();
    public void playSong()
    {
        player.reset();

        Song playSong = songs.get(songPosn);

        songTitle=playSong.getTitle();

        long currSong = playSong.getID();

        Uri trackUri = ContentUris.withAppendedId(android.provider.MediaStore.Audio.Media.EXTERNAL_CONTENT_URI, currSong);
        try
        {
            player.setDataSource(getApplicationContext(), trackUri);
        }
        catch(Exception e)
        {
            Log.e("MUSIC SERVICE", "Error setting data source", e);
        }
        player.prepareAsync();
    }

Nüüd tuleb meil palju lühikesi meetodeid, mis tagastavad meile meediafaili erinevad osad. getDur tagastab meediafaili pikkuse, isPng tagastab et meedia mängija mängib jne. 

    public void setSong(int songIndex)
    {
        songPosn=songIndex;
    }
    public int getPosn()
    {
        return player.getCurrentPosition();
    }

    public int getDur()
    {
        return player.getDuration();
    }

    public boolean isPng()
    {
        return player.isPlaying();
    }

    public void pausePlayer()
    {
        player.pause();
    }

    public void seek(int posn)
    {
        player.seekTo(posn);
    }

    public void go()
    {
        player.start();
    }

Siis loome meetodid, mis panevad meil mängima järgmise või eelmise meediafaili, sõltudes sellest, mis nupule kasutaja vajutab. Siis veel kaks meetodid, kus onDestory paneb meil äppi täielikult kinni, nii et meediafail ei mängi ka taustal, ning vajaliku meetodi, et kõik eelnev töötas ka siis, kui segastamine on pandud peale.

    public void playPrev()
    {
        songPosn--;
        if(songPosn<0) songPosn=songs.size()-1;
        playSong();
    }
    public void playNext()
    {
        if(shuffle){
            int newSong = songPosn;
            while(newSong==songPosn){
                newSong=rand.nextInt(songs.size());
            }
            songPosn=newSong;
        }
        else{
            songPosn++;
            if(songPosn>=songs.size()) songPosn=0;
        }
        playSong();
    }
    @Override
    public void onDestroy()
    {
        stopForeground(true);
    }
    public void setShuffle()
    {
        if(shuffle) shuffle=false;
        else shuffle=true;
    }}

### MainActivity.java

Nüüd võtame viimaks käsile MainActivity klassi. (NB! MainActivity-sse tuleb tegelikult vahetevahel lisada asju, mitte kõik korraga, seega on järjekord segamini)

Loome vajalikud muutujad ja onCreate meetodit muudame väheke, et meil küsitaks ligipääsu kasutaja telefoni meediafailide ligi.

`public class MainActivity extends AppCompatActivity implements MediaPlayerControl
{
    private ArrayList<Song> songList;
    private ListView songView;
    private MusicService musicSrv;
    private Intent playIntent;
    private boolean musicBound=false;
    private MusicController controller;
    private boolean paused=false, playbackPaused=false;`

    @Override
    protected void onCreate(Bundle savedInstanceState)
    {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.M)
        {
            if (checkSelfPermission(Manifest.permission.READ_EXTERNAL_STORAGE)!= PackageManager.PERMISSION_GRANTED)
            {
                requestPermissions(new String[]{Manifest.permission.READ_EXTERNAL_STORAGE},1);
                return;
            }
        }

Siis loome ja otsime üles meediafailide nimekirja.

        songView = (ListView)findViewById(R.id.song_list);
        songList = new ArrayList<Song>();
        getSongList();

        Collections.sort(songList, new Comparator<Song>()
        {
            public int compare(Song a, Song b)
            {
                return a.getTitle().compareTo(b.getTitle());
            }
        });
        SongAdapter songAdt = new SongAdapter(this, songList);
        songView.setAdapter(songAdt);

        setController();
    }

Siis loome teenuse meetodi, kuhu sisse teeme paar Override meetodit, et saada kätte meie teenus ja meediafailide list. Samuti, kuidas reageerida, kui tahame selle hoopis kinni panna.

    private ServiceConnection musicConnection = new ServiceConnection()
    {
        @Override
        public void onServiceConnected(ComponentName name, IBinder service)
        {
            MusicBinder binder = (MusicBinder)service;
            //get service
            musicSrv = binder.getService();
            //pass list
            musicSrv.setList(songList);
            musicBound = true;
        }

        @Override
        public void onServiceDisconnected(ComponentName name)
        {
            musicBound = false;
        }
    };

Siis loome meetodi, mis võtab meie meediafailide nimekirja ning seal otsime üles meediafailide id, pealkirja ja autori.
Samuti lisame Override meetodi, et kui äpp tööle läheb, hakkavad meie teenused tööle.
Siis meetodi, mis deklareerib ära, mis meediafail on valitud kasutaja poolt, ning paneb selle kohe mängima.

    public void getSongList()
    {
        ContentResolver musicResolver = getContentResolver();
        Uri musicUri = android.provider.MediaStore.Audio.Media.EXTERNAL_CONTENT_URI;
        Cursor musicCursor = musicResolver.query(musicUri, null, null, null, null);

        if(musicCursor!=null && musicCursor.moveToFirst())
        {
            int titleColumn = musicCursor.getColumnIndex(android.provider.MediaStore.Audio.Media.TITLE);
            int idColumn = musicCursor.getColumnIndex(android.provider.MediaStore.Audio.Media._ID);
            int artistColumn = musicCursor.getColumnIndex(android.provider.MediaStore.Audio.Media.ARTIST);
            do {
                long thisId = musicCursor.getLong(idColumn);
                String thisTitle = musicCursor.getString(titleColumn);
                String thisArtist = musicCursor.getString(artistColumn);
                songList.add(new Song(thisId, thisTitle, thisArtist));
            }
            while (musicCursor.moveToNext());
        }
    }
    @Override
    protected void onStart()
    {
        super.onStart();
        if(playIntent==null)
        {
            playIntent = new Intent(this, MusicService.class);
            bindService(playIntent, musicConnection, Context.BIND_AUTO_CREATE);
            startService(playIntent);
        }
    }
    public void songPicked(View view)
    {
        musicSrv.setSong(Integer.parseInt(view.getTag().toString()));
        musicSrv.playSong();
        if(playbackPaused){
            setController();
            playbackPaused=false;
        }
        controller.show(0);
    }

Nüüd loome veel Override meetodeid, kus hakkavad tööle meie layout inflaterid, et saaks menüüs navigeerida;Samuti meetodi, et otsustada mis juhtub, kui kasutaja millelegi vajutab; Siis jälle onDestroy meetodi, et kõik kinni panna; Meetodi, mis paneb meile äppi tööle; Meetodi ka, mis läheb pausile; Meetodi, mis otsib meie meediafaili pikkuse; Hetkese positsiooni; Meetodi, mis otsib meie positsiooni; Meetodi, mis katkestab meil helifaili mängimise, kui teenust ei saa; Ning lõpuks meetodeid, mis tagastavad meile vajalikud alg-vastused;

    @Override
    public boolean onCreateOptionsMenu(Menu menu)
    {
        MenuInflater inflater = getMenuInflater();
        inflater.inflate(R.menu.main, menu);
        return true;
    }
    @Override
    public boolean onOptionsItemSelected(MenuItem item)
    {
        switch (item.getItemId())
        {
            case R.id.action_shuffle:
                musicSrv.setShuffle();
                break;
            case R.id.action_end:
                stopService(playIntent);
                musicSrv=null;
                System.exit(0);
                break;
        }
        return super.onOptionsItemSelected(item);
    }
    @Override
    protected void onDestroy()
    {
        stopService(playIntent);
        musicSrv=null;
        super.onDestroy();
    }

    @Override
    public void start()
    {
        musicSrv.go();
    }

    @Override
    public void pause() {
        playbackPaused=true;
        musicSrv.pausePlayer();
    }

    @Override
    public int getDuration()
    {
        if(musicSrv!=null && musicBound && musicSrv.isPng())
        return musicSrv.getDur();
     else return 0;
    }
    @Override
    public int getCurrentPosition()
    {
        if(musicSrv!=null && musicBound && musicSrv.isPng())
        return musicSrv.getPosn();
     else return 0;
    }
    @Override
    public void seekTo(int pos)
    {
        musicSrv.seek(pos);
    }

    @Override
    public boolean isPlaying()
    {
        if(musicSrv!=null && musicBound)
        return musicSrv.isPng();
        return false;
    }

    @Override
    public int getBufferPercentage() {
        return 0;
    }

    @Override
    public boolean canPause()
    {
        return true;
    }

    @Override
    public boolean canSeekBackward()
    {
        return true;
    }

    @Override
    public boolean canSeekForward()
    {
        return true;
    }

    @Override
    public int getAudioSessionId()
    {
        return 0;
    }

Nüüd loome mõned tavalised meetodid. Kõigepealt ühe, mis paneb meil mõned funktsioonid MusicController klassiga tööle.
Meetodi, mis paneb meil mängima järgmise meediafaili, ning meetodi, mis teeb sama, aga paneb mängima hoopis eelneva meediafaili.

    private void playNext()
    {
        musicSrv.playNext();
        if(playbackPaused){
            setController();
            playbackPaused=false;
        }
        controller.show(0);
    }

    private void playPrev()
    {
        musicSrv.playPrev();
        if(playbackPaused){
            setController();
            playbackPaused=false;
        }
        controller.show(0);
    }

Ning lõpuks loome veel mõned Override meetodid pausi jaoks, jätkamise jaoks ja lõpetamise jaoks.

    @Override
    protected void onPause()
    {
        super.onPause();
        paused=true;
    }
    @Override
    protected void onResume()
    {
        super.onResume();
        if(paused){
            setController();
            paused=false;
        }
    }
    @Override
    protected void onStop()
    {
        controller.hide();
        super.onStop();
    }}

# Tuntumad vead
_1. Kui vajutada mingile meediafailile, hakkab meediafail küll mängima, kuid meedia mängija allpool ei muutu üldse, oleks nagu kinni jooksnud. Seda saab parandada, kui korra vajutada meediafail mängijal pausile, ning seejärel jätkata. See parandab selle väikse vea ära._

# Prototüüp
[Viide](https://app.moqups.com/janerik000@gmail.com/NYLyzk0TK4/view) (Varajane)
