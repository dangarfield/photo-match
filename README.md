# Photo Booth
> Facial Recognition system with auto indexing and allocation in real time. Machine learning at the edge

![alt text](https://image.ibb.co/eHBaTL/Screen-Shot-2018-10-31-at-21-56-46.png "photo booth")

### Accuracy Stats
- Embarkation (cabin) - __100% accuracy__ for pictures allocated to the correct cabin (127 of 127 pictures) - Day 1 Palma 11am Embark
- Embarkation (face) - __95% accuracy__ for all faces (267 of 280 pictures) - Day 1 Palma 11am Embark
- Portraits (cabin) - __93% accuracy__ for pictures allocated to the correct cabin (195 of 210 pictures) - Day 2 Latitude Portraits 8pm
- Portraits (face) - __85% accuracy__ for all faces (393 of 461 pictures) - Day 2 Latitude Portraits 8pm
- _Note: This is based on a random choice of two photoshoots (~350 photos), with 1 passenger registration error not fixed_

### Key Features
- +93% accuracy for matching photographs to the cabins
- Simple responsive customer facing user interface for photo selection, product selection and checkout process
- All registration and portrait images are processed in realtime, 3 secs per image and instantly available to customers
- Admin area for maintenance, content management, shop management, registration and portrait image error correction / allocation
- Built on 38 APIs in 3 services, easily extensible

### Demo
- Open site: http://photomatch.tui-maker-fair.co.uk
- Real life demo
  - Before demo, remove all registration files for 123, 1234, 1235 cabins & test allocation folders (in admin files section)
  - Take photos of two people for registration. Note: ensure landscape, as mobiles tend to mess around with EXIF rotation data and you'll have to edit the photo rotation manually
    - 1 - Good photo, 1 person in photo, clear background
    - 2 - 1 person in foreground, 1 in background
  - Take photos of the two people together with different facial expressions (eg, portrait)
  - Upload photo to presenting laptop (dropbox etc), or share your mobile screen onto the projector
  - Upload registration photos
    - Go to admin upload section
    - Choose files - attach the two registation photos
    - Ensure that the both users are in 123 cabin (set cabin number, passenger id and names accordingly, must be unique)
    - Click upload
    - Wait about for 10 seconds (can look at the status page and wait until)
  - Look at cabin (new tab)
    - Navigate to select passenger front end and select cabin 123 from the dropdown
    - Only one registration image was processed because the other was invalid and therefore, only one person is shown in the cabin
  - Go to admin registration errors section
    - Find the uploaded registration image
    - Using the cropping tool, crop the main user until it says 'valid'
    - Click save
    - Wait 5 seconds
  - Look at cabin (refresh page)
    - Both users are now in the cabin
  - Upload portrait photos
    - Go to admin upload section, choose files and upload, ensure in Test folder
    - Wait 10 seconds
  - Look at cabin (refresh page)
    - Both users are identifed
- Show homepage
  - Highlight product merchandising
  - Highlight typeahead with passenger names and cabin number (Passenger names will be replaced with real names)
- Show image selection: Pick random cabins (eg 12000-12010, 10100-10150, 8010-8030) - I suggest finding a good few with a few good pictures
  - Highlight registration image (hover over individual names in nav)
  - Highlight passenger filtering (click on individual names AND view all cabin)
  - Highlight selecting one image
    - Highlight fullscreen image
    - Highlight face recognition
    - Click add to basket (add a few images)
  - Go to another cabin and add another photo to the basket (eg, baskets are not specific to cabins)
- Show order
  - Click 'basket' icon in top-right
  - Highlight payee -> can be changed
  - Highlight product merchandising
  - Highlight product selection
    - Highlight + & -
    - Highlight multibuy discount price changes across photos
    - Highlight hidden discretionary discount
    - Checkout
    - Highlight printable order invoice
- Show admin area (new tab) - Optional if there is time
  - Highlight status dashboard - Highlights images, process queues and server status
  - Highlight product setup -> eg, Change price on homepage for 12 x 8
  - Highlight Styling -> eg, change # SELECT PASSENGER pas.title
  - Highlight orders
  - Highlight upload (in live demo)
  - Highlight files (in live demo)
  - Highlight registation errors (in live demo)
  - Highlight allocation errors -> eg, these have no matches, some images are just difficult to match, can be fixed with manual allocation
  - Highlight manual allocation
    - Randomly select images from dropdown - Ensure that you them from a few different phoots (eg, not just embarkation)
    - Highlight plus & minus
    - Highlight assigned cabin ids = Probably the right people
    - Highlight whitelist & blacklist

### Extras that are not complete / requested - Pending DigiTech / TUI requirements
- Detailed product and pricing setup
- Later Phase - Shopware integration - For product, price and order management
- Registration Image Validation in port terminal (eg, Registration Laptop -> Validation Service) - Ensure that registration images are valid at terminal in real-time, before sending to resco / photo server
- Personalised digital signage - As people walk past, we show their portrait photos. Many other applications, eg Coffee shop & predictions
- Ensure validity of exported data for offline / post cruise selling - eg, validate APIs and relative paths for photos
- Back-to-back cruise customers see all photos across all cruises - eg, ensure that each 'week' is archived without causing performance issues
- Consume Resco API for retrieving customer name
- Consume Resco event (if available) for triggering cabin change
- Order list admin screen shows summary and status

### All Features
- 3 core services - Recognition engine, api & data integration layer, photo booth web application
- Facial recognition is up to 87% accurate with trained image sets complete on TUI cruises
- Automatically extracts cabin, passenger name and passenger id data from registration images
- Automatically loads, indexes and processes registration data in real time as changes are made / added / remove registration images
- Registration images are cropped, faces extracted from highly accurate face matching model
- Processed registration images are stored in a constantly updating model
- Facial machine learning models, facial features and api data sets are persisted to disk and run automatically on server startup
- Registration facial recognition failures (due to bad photos / lighting, multiple faces in photo) are easily and quickly solvable in a bundled admin tool that allows for quick and manual non-disruptive cropping, with instant facial recognition success feedback
- Automatically loads photographs to be allocated to registered faces in real time as images are added / removed / amended in a shared file directory
- Allocated errors are displayed in a admin tool for evaluation (eg, no matches)
- Manual allocation admin tool that allows whitelisting and blacklisting of passengers to any given image with typeahead support, updated in real time
- Indexing and allocation is processed through a queueing system to ensure no partial updates and recover from application failures on restart
- Status and admin action console for triggering basic maintenance tasks
- All actions and data triggerable through documented APIs
- Price and product administration is done through a portal, any number and type of products can be created, including descriptions, advertising blurb and also configuration of the pricing 'banner' on the homepage
- Prices can be set per item and also offer a lower price for buying multiple products
- Web application for passengers to quickly typeahead search using their cabin, passenger name, passenger id
- Web application groups photos by cabin and passenger, showing thumbnails of all, including registration images
- Web application allows displaying of facial recognition bounding boxes in a 'facebook like' tagging mechanism
- Web application allows for adding photographs to cart
- Web application allows for users to choose what multiple types of configured products and prints for each of their photographs
- Web application allows for multi-buy discounts of the same product type to be split over multiple photographs
- Web application allows for hidden discretionary discount for the retail agent
- Web application show printable order invoice for customer
- All orders can be viewed and opened from the admin portal
- All orders are saved in extractable order files for processing in downstream applications
- 38 APIs developed for all aspects of recognition, web application content and administration tasks. Every item of functionality is backed by an API
- APIs documented in postman collection - [/api/documentation](/api/documentation)
- APIs include change cabin request. All registration and photo allocations are updated
- Admin area allows for user amended localised text (Content Management) for all customer facing text
- Admin area allows for overriding any CSS styling rules
- Admin area allows for replacing the site logo

### Installation
- Standard docker installation
- CPU requirements - 4 CPUs recommended
- Memory requirements - 8GB recommended
- IO requirements - As the data and image directories will be external to the docker application, a good level of IOPS, latency, throughput is required
- Pull image from private docker registry using Koa Consult provided credentials - `docker pull registry.gitlab.com/koa-consult/photo-match`
- Run with specified mount points:
```bash
docker run \
  --name photo-match \
  -p 80:3000 \
  -d \
  --cpus 4 \
  -m "8gb" \
  --mount type=bind,source="/shared-folder/data",target=/app/data \
  --mount type=bind,source="/shared-folder/images",target=/app/images \
  -it registry.gitlab.com/koa-consult/photo-match
```
- If these external mount points are not created, the app will create the folders inside the container. Photos will have to be uploaded in the admin section manually. Note: All data on a container is ephemeral and will be lost once the container is shut down. If this is case, it is suggested to run in detached mode. Standard `docker cp` can be used to transfer files to and from the container as the administrator requires
- The internal port that needs to be exposed is 3000
- If the application sits behind a proxy, standard HTTP methods GET, POST and DELETE must be exposed. Websockets may also be exposed in future releases
- Standard `docker` and `pm2` monitoring commands apply, eg:
```bash
docker stats photo-match
docker exec -it photo-match pm2 monit
docker exec -it photo-match pm2 logs
```
- Registration file conventions:
  - PHOTO_{cabinNo}_{passengerId}_{date}.{ext}
  - eg, PHOTO_1235_91000_2018-10-13_11-09-55.jpg
  - cabinNo - alpha numeric only
  - passengerId - alpha numeric only
  - date - alpha numeric only, this is not parsed or used presently within the app
  - ext - jpg, jpeg, png
  - Passenger name - `TBC`
- Portrait photography conventions
  - Use jpg, jpeg, png
  - Add in nested subfolders for convenience and improved performance



### Usage Instructions
- tbc

### Todo
- ~~Admin - Typeahead input UI colouring~~
- ~~Admin - All blurb for usage in all screens~~
- ~~Admin - Add action buttons~~
- ~~Booth - Change customer cabin selection to url based~~
- ~~Booth - Add easy 'select new cabin / passenger'~~ - Maybe later
- ~~Booth - TUI oriented UI and colouring~~ - Fine as green, change to red and blue is a lot of effort
- ~~Booth - Declutter text in hover overlay~~
- ~~Pricing admin console~~
- ~~Customer facing pricing overview~~
- ~~Pricing add to basket~~
- ~~Pricing cart total and checkout button fixed on right hand side~~
- ~~Pricing checkout -> Order~~
- ~~Order management and overview~~
- ~~Upload registration and photography photo API~~
- ~~Upload registration and photography admin portal~~
- ~~Problem images, eg, photo collage backgrounds with 'people' that shouldn't be matched~~ - This can be achieved by manually adding images, test with this data set
- ~~Get accurate levels by doing 2x 100 photo tests~~
- ~~Configuration through environment variables~~ - Not needed any more
- ~~Ensure all APIs in postman~~
- ~~Add API descriptions~~ - Nah, can add another day if required
- ~~Swagger file for APIs~~ - Nah, kept it simple with postman
- ~~Externalise data folders~~
- ~~Docker packaging (3 images vs 1 etc)~~
- ~~Gitlab deploy tokens - saved in deploy-tokens.txt~~
- ~~Docker 'cmd' for execution on start~~
- ~~Docker test mounted directories~~ Fine, but massive performance issues in terms of IO on Mac, need to test on linux
- ~~Docker deployment instructions including deploy token keys~~
- ~~Find out why there is a 1 count in the photography and registration (should be 0 when empty)~~
- ~~Set 'allocate with registration images failures' back to stop for prod~~
- ~~Turn scan-all back on for prod~~
- ~~Validate data folders are correctly setup on server startup~~
- ~~Define registration and photography naming and file requirements~~
- ~~Add infrastructure and server setup instructions~~
- ~~Deploy and test in real life~~
- ~~Add localisation and text amending~~
- ~~Add custom css rules~~
- ~~Add custom logo~~
- ~~Update features to include localisation, css and logo editing~~
- ~~Externalise theme folders~~ - Don't need to do now that it is editable via API
- ~~Get oxygen font local~~

- Add usage instructions & videos

- Ensure the test data can be uploaded and ran in AWS container
- Add license info about mental UI
- Time sheets
- Add production servers
- Add build process for obsfuscated js and python
- Move pricing logic to server side
- £ signs, move to locales
- Remaining JS items for alerts and typeahead, move to locales

- Order syndication and API integration
- Get passenger names through EXIF / file names, update read.me conventions

- Add API for posting image directly to :3000 for prediction
- Facial recognition for users walking past, eg, digital signage or at kiosk login

- Resco API - Get customer name
- Resco API - Change cabin
- Fully Responsive
