# Clean Code

> “Any fool can write code that a computer can understand. Good programmers write code that humans can understand.” – [Martin Fowler](https://apiumhub.com/tech-blog-barcelona/microservices-vs-monolithic-architecture/).

Clean Code merupakan gaya penulisan kode program yang  bertujuan menghasilkan perangkat lunak yang mudah untuk ditulis, dibaca, dan dipelihara. Clean code juga bisa diartikan sebagai kode program yang mudah dipahami dan mudah diubah.

Beberapa alasan mengapa clean code begitu penting:

- Clearness

  Sangat mudah untuk melupakan arti dari tiap kode program yang telah ditulis. Karenanya setiap pengembang harus membuat kode program sebersih dan sejelas mungkin. Penulisan kode program harus seperti seorang penulis yang menceritakan sebuah kisah di dalam sebuah buku. Mereka menggunakan bab, judul, dan paragraf yang jelas untuk bisa membimbing pikiran pembacanya masuk kedalam alur cerita. Proses penulisan kode program tidak jauh berbeda seperti itu, tetapi menggunakan namespaces, classes, dan metode, bukan kata.

- Maintenance

  Menulis sebuah kode program relatih mudah, namun tidak semua kode program yang telah ditulis mudah untuk dibaca. Karenanya lebih banyak pengembang lebih memilih untuk menulis ulang sebuah kode program daripada menterjemahkan sebuah kode program.  Dengan menerapkan Clean code kita bisa menghemat lebih banyak waktu dalam proses pengembangan aplikasi. Sebab kode program sudah memiliki standar dalam proses pembuatannya. Sehingga mengindari penulisan kode program yang buruk.

- Easy to Test

  Penerapan Clean code dapat membatu pada tahap pengujian aplikasi. Seperti pada tahap pengujian Test-Driven-Development(TDD) yang merupakan cara paling efektif dalam meningkatkan kualitas suatu kode program.  Dengan kode yang lebih rapi membuatnya mudah untuk diuji dan dibaca

- Simplicity

  Dengan membuat aplikasi lebih sederhana, dapat menghasilkan kode program berkualitas tinggi, dapat menyelesaikan masalah lebih cepat, dan membatu bekerja lebih baik di dalam tim.

### How to Create Meaningful Names

Proses penamaan pada saat penulisan kode program mungkin terdengar mudah. Namun apakah penamaan tersebut sudah tepat? Pada konsep clean code penamaan sebuah variable, classes, functions, arguments atau packages tidak boleh sembarangan. Sebuah nama harus bisa menjelaskan keberadaannya, berfungsi sebagai apa, dan bagaimana cara kerjanya.



>  "A name should tell you why it exists, what it does, and how it is used." – Clean Code



Mungkin akan memerlukan waktu yang lebih lama untuk menemukan sebuah nama yang tepat, namun itu akan lebih menghemat banyak waktu bagi anda dan tim di masa mendatang.

Berikut beberapa cara dalam pembuatan sebuah nama yang baik di dalam pembuatan suatu kode program :

1. Use name to reveal the intent

   Jika sebuah nama memerlukan komentar untuk menjelaskan fungsinya, maka gunakan penjelasan itu sebagai sebuah nama.

   **Bad**

   ```java
   int d // elapsed time in days
   ```

   **Good**

   ```java
   int elapsedTimeInDays
   int daySinceCreation
   int fileAgeInDays
   ```

   

2. Use Intention-Revealing Names

   Dalam memberikan sebuah nama, gunakan nama yang lebih menjelaskan

   **Bad**

   ```java
   public List<int[]> getThem(){
       List<int[]> list1 = new ArrayList<int[]>();
       for(int[] x : theList)
           if (x[0] == 4)
               list1.add(x);
       return list1
   }
   ```

   **Good**

   ```java
   public List<Cell> getFlaggedCells(){
       List<Cell> FlaggedCells = new ArrayList<Cell>();
       for(Cell cell : gameBoard)
           if (cell.isFlagged)
               FlaggedCells.add(cell);
       return FlaggedCells
   }
   ```

   

3. Prounanceable Names

   **Bad**

   ```java
   class dtaRcrd02{
       private Date genymdhms;
       private Date modymdhms;
       private final String pszqint = "102";
       /* ... */
   };
   ```

   **Good**

   ```java
   class Customer{
       private Date generationTimestamp;
       private Date modificationTimestamp;
       private final String recordId = "102";
       /* ... */
   };
   ```

4. Searchable name

   **Bad**

   ```java
   for(int j=0; j<34; j++){
       s += (t[j]*4)/5
   }
   ```

   **Good**

   ```java
   int realDaysPerIdealDay = 4;
   const int WORK_DAYS_PER_WEEK = 5
   int sum = 0
   for (int j=0; j < NUMBER_OF_TASKS; j++){
       int realTaskDays = taskEstimate[j] * realDaysPerIdealDay;
       int realTaskWeeks = (realdays / WORK_DAYS_PER_WEEK);
       sum += realTaskWEeks;
   }
   ```

5. Class names

   Penamaan class dan object harus menggunakan kata benda atau satu frasa kata benda seperti Customer, WikiPage, Account, atau AddressParser. Jangan gunakan kata kerja untuk penamaan sebuah class.

6. Method Names

   Berbeda dengan class, untuk penamaan method gunakanlah kata kerja atau satu frasa kata kerja seperti postPayment, deletePage, atau save.

7. Pick one word per concept

   Pilihlah satu kata untuk satu buah proses. Akan sangat membingungkan bila terdapat beberapa kata yang memiliki arti yang hampir mirip dalam sebuah method. Seperti fetch, retrieve, dan get jika digunakan sebagai prefix suatu method meski berbeda class akan sangat menyulitkan. Terkadang kita akan lupa method apa yang harus digunakan.

   

> Say what you mean. Mean what you say.



## Functions

> Clarity is King – Clean Code

1. They should be small

   Aturan pertama dalam pembuatan function adalah buat sependek mungkin. Aturan nomor dua, buatlah lebih pendek lagi.

   **Bad**

   ```java
   private void listener(ConsumerRecords<String, String> data){
       for(ConsumerRecord<String, String> record : data) {
           JSONObject resultObj = parserService.run(record);
   
           if(resultObj.getBoolean("status")) {
               JSONObject dataObj = resultObj.getJSONObject("data");
               if (application.getStatus().equals("production")) {
                   if (dataObj.getBoolean("ambassador") == true && dataObj.getBoolean("official_ambassador") ==true){
                       final CredentialsProvider credentialsProvider = new BasicCredentialsProvider();
                       RestClientBuilder builder = RestClient.builder(new HttpHost(elasticsearch.getClusterNodes().split(":")[0], Integer.parseInt(elasticsearch.getClusterNodes().split(":")[1])))
                       .setRequestConfigCallback(new RestClientBuilder.RequestConfigCallback() {
                           @Override
                           public RequestConfig.Builder customizeRequestConfig(RequestConfig.Builder builder) {
                               return builder
                                       .setConnectTimeout(180000)
                                       .setSocketTimeout(300000);
                           }
                       });
                       RestHighLevelClient client = new RestHighLevelClient(builder);
   
                       IndexRequest request = new IndexRequest().index("brand-catalog-ambassador-post").type("_doc").id(result.get("id").toString());
                       request.source(result.toMap());
                       IndexResponse indexResponse = client.index(request, RequestOptions.DEFAULT);
   
                       client.close();
   
                       elasticService.insertBrandCatalog(dataObj);
                   }
                   kafkaTemplate.send(kafka.getProducer().getTopic(), dataObj.toString());
               }else{
                   logger.info("[!] Data : added [Devel]");
               }
           }
       }
   }
   ```

   **Good**

   ```java
   private void kafkaConsumer(ConsumerRecords<String, String> records){
       for(ConsumerRecord<String, String> record : records) {
           JSONObject resultObj = parserService.run(record);
   
           if(isResultStatusTrue(resultObj)) {
               JSONObject dataObj = resultObj.getJSONObject("data");
               if (isApplicationStatusTrue(application.getStatus())) {
                   if (fieldPostCategoryOfficialAmbassadorExist(dataObj)){
                       elasticService.insertBrandCatalog(dataObj);
                   }
                   elastic.send(kafka.getProducer().getTopic(), dataObj.toString());
               }else{
                   logger.info("[!] Data : added [Devel]");
               }
           }
       }
   }
   ```

   

2. Do one thing

   Buatlah satu function hanya untuk mengerjakan satu proses saja. Jika dilihat Bad code pada point satu terdapat 2 proses yang dilakukan. Proses mengirimkan data ke elastic dan kafka. Dengan menaruh dua proses itu di dalam satu function code akan terlihat penuh. Proses pembuatan koneksi ke database pun dilakukan berulang kali. Dengan mengubah function seperti Good code pada point satu akan membuat code lebih mudah untuk dibaca dan proses pun lebih efisien.

3. Use descriptive names

   Pada contoh Good code diatas, kita merubah mengubah nama function dari **listener** menjadi **kafkaConsumer**. Selain itu kita juga mengubah conditional statements menjadi sebuah function tersendiri. Dengan melakukan seperti halnya di atas akan membantu dalam memahami maksud dan proses code itu sendiri.

4. Extract try/catch blocks

   ```java
   try{
       deletePage(page);
       registry.deleteRefrence(page.name);
       configKeys.deleteKey(page.name.makeKey())
   }catch(Exception e){
       logger.log(e.getMessage())
   }
   ```

   Struktur code di atas mungkin sangat sering kita gunakan.  Menaruh beberapa proses pada satu block try/catch. Seperti yang telah di jelaskan pada point dua, function harus mengerjakan satu proses saja. Error handling terhitung sebagai satu proses. Karenanya kita harus memecahnya. Kita dapat membuatnya menjadi lebih baik seperti struktur code di bawah ini:

   ```java
   public void delete(Page page){
       try{
           deletePageAndAllReferences(page);
       }catch(Exception e){
           logError(e)
       }
   }
   
   private void deletePageAndAllReferences(Page page) throws Exception{
       deletePage(page);
       registry.deleteRefrence(page.name);
       configKeys.deleteKey(page.name.makeKey())
   }
   
   private void logError(Exception e){
       logger.log(e.getMessage)
   }
   ```

   Dengan mengubah mengubah code seperti struktur di atas akan membuat code menjadi lebih mudah dibaca dan di modifikasi.

   > Master programmers think of system as stories to be told rather than programs to be written.

## Comments

Dalam memahami suatu kode program, kehadiran comment sangat membantu dari salah persepsi. Beberapa comment memang dibutuhkan pada satu kode. Namun bukan berarti kita harus memberikan comment pada tiap proses agar tidak terjadi salah persepsi. Memberikan banyak comment tidak membuat kode program menjadi lebih baik. Perhatikan kode program di bawah ini:

```java
//Check to see if the employee is eligible for full benefits
if((employee.flags &  HOURLY_FLAG) && (employee.age > 65))
```

Daripada menggunakan comment untuk menjelaskan maksud dari suatu proses di atas lebih baik gunakan penamaan yang lebih jelas seperti di bawah ini :

```java
if(employee.isEligibleForFullBenefits())
```

Lalu seperti apa comment yang baik itu ?

1. Legal Comments

   ```java
   // Copyright (C) 2003,2004,2005 by Object Mentor, Inc. All rights reserved
   // Released under the terms of the GNU General Public Lisence version 2 or later.
   ```

2. informative comment

   ```java
   // Return an instance of the Responder being tested
   protected abstract Responder responderInstance();
   ```

   ```java
   // format matched yyyy-MM-dd
   Pattern timeMatcher = Pattern.complie("\\d*-\\d*-\\w*")
   ```

3. Explain of Intent

   ```java
   //This is our best attempt to get a race condition
   //by creating large number of threads.
   for(int i = 0; i < 25000; i++){
       WidgetBuilderThread widgetBuilderThread = new WidgetBuilderThread;
       Thread thread = new Thread(widgetBuilderThread);
       thread.start;
   }
   
   ```

4. Clarification

   ```java
   public void testCompareTo(){
       WikiPagePatch a = PathParser.parse("PageA");
       WikiPagePatch ab = PathParser.parse("PageA.PageB");
       WikiPagePatch b = PathParser.parse("PageB");
       WikiPagePatch aa = PathParser.parse("PageA.PageA");
       WikiPagePatch bb = PathParser.parse("PageB.PageB");
       WikiPagePatch ba = PathParser.parse("PageB.PageA");
       
       assertTrue(a.compareTo(a) == 0); // a == a
       assertTrue(a.compareTo(b) != 0); // a != b
       assertTrue(ab.compareTo(ab) == 0); // ab == ab
       assertTrue(a.compareTo(b) == -1); // a < b
       assertTrue(aa.compareTo(ab) == -1); // aa < ab
   }
   ```

5. Warning of consequences

   ```java
   public static simpleDateFormat makeStandartHttpDateFormat(){
       //SimpleDateFormat is not thread safe,
       //so we need to create each instace independently
       SimpleDateFormat df = new SimpleDateFormat("yyyy-MM-dd");
       df.setTimeZone(TimeZone.getTimeZone("GMT"));
       return df
   }
   ```

6. TODO Comments

   ```java
   //TODO-mdm these are not needed
   //We expect this to go away when we do the checkout model
   protect Version makeVersion(){
       return null
   }
   ```

   

> Don't comment bad code–rewrite it. –Brian W. Kernighan and P. J. Plaugher

## Classes

1. Classes should be small

   Sama halnya dengan function aturan pertama dalam pembuatan class adalah buat sependek mungkin. Aturan nomor dua, buatlah lebih pendek lagi. Pada function kita mengukur panjangnya berdasarkan jumlah line. Berbeda dengan class, kita melihatnya berdasarkan responsibilities.

   **Bad**

   ```java
   public class socialMediaMapper{
       private void mapperDataFacebook(JSONObject obj) {/**Any process*/}
       
       private void mapperDataInstagram(JSONObject obj) {/**Any process*/}
       
       private void mapperDataYoutube(JSONObject obj) {/**Any process*/}
       
       private void mapperDataTwitter(JSONObject obj) {/**Any process*/}
       
       protected List<Mention> parseMention(JSONArray jsonArray) {/**Any process*/}
   
       protected List<String> parseHashtag(JSONArray jsonArray) {/**Any process*/}
   
       protected List<Media> parseMedia(JSONArray jsonArray) {/**Any process*/}
   
       protected List<String> parseLink(JSONArray jsonArray) {/**Any process*/}
   
       protected List<String> parseDomains(JSONArray jsonArray) {/**Any process*/}
   
       protected List<String> parseMediaTags(JSONArray jsonArray) {/**Any process*/}
   
       protected List<String> parseAnnKeywords(JSONArray jsonArray) {/**Any process*/}
   
       protected List<String> parseAnnLocation(JSONArray jsonArray) {/**Any process*/}
   
       protected List<String> parseAnnPerson(JSONArray jsonArray) {/**Any process*/}
   
       protected List<String> parseAnnOrganization(JSONArray jsonArray) {/**Any process*/}
       protected List<String> parseAnnPhrase(JSONArray jsonArray) {/**Any process*/}
   
       protected List<String> parseAnnWordList(JSONArray jsonArray) {/**Any process*/}
   
       protected List<Location> parseLocation(JSONArray jsonArray) {/**Any process*/}
   
       protected Location parseLocationDefault(JSONObject obj) {/**Any process*/}
   
       protected List<String> parsePostImage(List<Media> medias) {/**Any process*/}
   
       protected List<String> parsePostVideo(List<Media> medias) {/**Any process*/}
   
       protected String convertObjectToJsonString(Object obj) throws JsonProcessingException {/**Any process*/}
   
       protected Location parseUserLocation(JSONObject annotation) {/**Any process*/}
   
       protected List<Work> parseWork(JSONArray obj) {/**Any process*/}
   }
   ```

   Dari code di atas bisa dilihat bahwa  class **socialMediaMapper** mengemban banyak sekali responsibilities. Kita bisa membuatnya menjadi lebih simpel seperti contoh di bawah ini:

   **Good**

   ```java
   public class socialMediaMapper extends MappingUtils {
       private void mapperDataFacebook(JSONObject obj) {/**Any process*/}
       
       private void mapperDataInstagram(JSONObject obj) {/**Any process*/}
       
       private void mapperDataYoutube(JSONObject obj) {/**Any process*/}
       
       private void mapperDataTwitter(JSONObject obj) {/**Any process*/}
   }
   ```

   ```java
   public class MappingUtils {
       protected List<Mention> parseMention(JSONArray jsonArray) {/**Any process*/}
   
       protected List<String> parseHashtag(JSONArray jsonArray) {/**Any process*/}
   
       protected List<Media> parseMedia(JSONArray jsonArray) {/**Any process*/}
   
       protected List<String> parseLink(JSONArray jsonArray) {/**Any process*/}
   
       protected List<String> parseDomains(JSONArray jsonArray) {/**Any process*/}
   
       protected List<String> parseMediaTags(JSONArray jsonArray) {/**Any process*/}
   
       protected List<String> parseAnnKeywords(JSONArray jsonArray) {/**Any process*/}
   
       protected List<String> parseAnnLocation(JSONArray jsonArray) {/**Any process*/}
   
       protected List<String> parseAnnPerson(JSONArray jsonArray) {/**Any process*/}
   
       protected List<String> parseAnnOrganization(JSONArray jsonArray) {/**Any process*/}
       protected List<String> parseAnnPhrase(JSONArray jsonArray) {/**Any process*/}
   
       protected List<String> parseAnnWordList(JSONArray jsonArray) {/**Any process*/}
   
       protected List<Location> parseLocation(JSONArray jsonArray) {/**Any process*/}
   
       protected Location parseLocationDefault(JSONObject obj) {/**Any process*/}
   
       protected List<String> parsePostImage(List<Media> medias) {/**Any process*/}
   
       protected List<String> parsePostVideo(List<Media> medias) {/**Any process*/}
   
       protected String convertObjectToJsonString(Object obj) throws JsonProcessingException {/**Any process*/}
   
       protected Location parseUserLocation(JSONObject annotation) {/**Any process*/}
   
       protected List<Work> parseWork(JSONArray obj) {/**Any process*/}
   }
   ```

2. The Single Responsibility Principle

   The Single Responsibility Principle(SRP) merupakan sebuah prinsip yang mengharuskan sebuah class hanya boleh memiliki satu responsibility. Jika kita lihat class **socialMediaMapper** pada Good code di point satu, masih terdapat empat responsibility pada class tersebut. Dengan menerapkan SRP, kita dapat membuatnya menjadi empat class di bawah ini :

   ```java
   public class facebookMapper extends MappingUtils {
       private void mapperDataFacebook(JSONObject obj) {/**Any process*/}
   }
   ```

   ```java
   public class instagramMapper extends MappingUtils {
       private void mapperDataInstagram(JSONObject obj) {/**Any process*/}
   }
   ```

   ```java
   public class youtubeMapper extends MappingUtils {
       private void mapperDataYoutube(JSONObject obj) {/**Any process*/}
   }
   ```

   ```java
   public class twitterMapper extends MappingUtils {
       private void mapperDataTwitter(JSONObject obj) {/**Any process*/}
   }
   ```

   

3. Organizing for Change

   Sebuah aplikasi pasti akan melakukan perubahan terus menerus. Beberapa perubahan berisiko membuat aplikasi kita tidak lagi berfungsi sebagaimana mestinya. Dalam membuat sistem yang baik, kami mengatur kelas kita untuk bisa mengurangi risiko perubahan.

   ```java
   public class sql{
       public Sql(String table, Column[] columns);
       public String selectAll();
       public String insert(Object[] fields);
       public String findByKey(String keyColumn, String keyValue);
       public String 
   }
   ```

   

> The problem is that too many of us think that we are done once the program works. We fail to switch to the other concern of organization and cleanliness.



## Error Handling

1. Use exceptions rather than return codes
   **Bad**

   ```java
   public class DeviceController{
       public void sendShutDown(){
           DeviceHandle handle = getHandle(DEV1);
           //check the state of the device
           if(handle != DeviceHandle,Invalid){
               //Save the device status to the record field
               retriveDeviceRecord(handle);
               
               //if not suspended, shut down
               if(record.getStatus() != DEVICE_SUSPENDED){
                   pauseDevice(handle);
                   clearDeviceWork(handle);
                   closeDevice(Handle);
               }else{
                   logger.log("Device Suspended. Unable to shut down");
               }
           }else{
               logger.log("Invalid Handle for : " + DEV1.toString());
           }
       }
   } 
   ```

   **Good**

   ```java
   public class DeviceController{
       public void sendShutDown(){
           try{
               tryToShutDown();
           }catch(Exception e){
               logger.log(e)
           }
       }
       
       private void tryToShutDown() throw DeviceShutDownError{
           DeviceHandle handle = getHandle(DEV1);
           Device Record = retriveDeviceRecord(handle);
           
           pauseDevice(handle);
           clearDeviceWork(handle);
           closeDevice(Handle);
       }
       
       private DeviceHandle getHandle(Device id){
           throw new DeviceShutDownError("Invalid Handle for : " + DEV1.toString())
       }
   }
   ```

   

2. Dont return null

3. Dont pass null