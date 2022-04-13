# FTX Demo
A nice little demo of an NFT collection viewer. Allowing users to view collections and NFT details. The overall project is primarily web, however, with some small tweaks is ready for Native platforms as well(due to use of React Native Web). More details down below.

**Live URL: https://ftxdemo-nateageek.netlify.app/

# Why XYZ package?
- craco: I needed to override some of the default Create React App scripts without ejecting. I firmly think that ejecting should be rarely done, as Create React App provides a good base to build your projects. There are a few other base project templates, such as Vite for example. Create React App is the most I am familiar with, and stuck with it.
- react-native-linear-gradient: Needed some nice gradients :D
- swr: I chose to go with SWR due to its caching approach for handling requests. For simplicity, if a custom hook is used, it will "cache" the contents of the requested payload and return the same data to components with the same hook call. This allows me to have a kinda effective global state with my api requests. Now typically if the projects requires a large complicated global state(like we had user logins and other complex shared state) I would go with Redux/Toolkit. I have also taken a liking to Redux Toolkit Query over my old approach with Redux-Saga. 
- twrnc: Actually this was my first project using TailwindCSS. I've always used Stylesheets or SCSS with my projects. Although, in others I've used similar tools like Foundation or Bootstrap, I did like TailwindCSS. Only drawback was I am using a React Native specific package and a lot of features I hope for were not supported due to the "Native" limitations. Some of these limitations included, grid, hover, animations. But it got the job done. I'm not sure if I would use twrnc again, just due to its implementation, however, I could see using it if it added the other features(aka I find time to make a PR).
- react-native-vector-icons: Just a quick way to grab some icons. I even create my own Crypto icon font base on CryptoFont. Might publish it as a little open source project.

# A to Z Approach
I have worked in fairly large and small teams (ranging from 2 - 8). I usally have different phases: Discovery, Design, and Implementation.

## Discovery
I had a FigmaJam brainstorm board, and time locked my session to about an hour. I came up with some cool ideas that I wanted to do to show some of my creative side. 

**FigmaJam Link: 

I wanted to create a platform for battling NFTs. I was going to implement a trade product where two people could battle their NFT. The objective is to bet that your nft would stay the same price or go higher than your opponents, you would basically barrow the opponents NFT and short it. Since we can view NFTs as having some value, you would use your own NFT as some initial collateral, and if your NFT crashed then you would probably have to cover. This product could be use as a general NFT market hedge. If both NFT crash at the same rate then you would come out neutral. If you made a wise bet with someone and the value of your NFT went up and theirs went down, you could make a good profit.

Overall sadly as I started to code and review the API, the complexity of the desired app, and the timeline, made the it a bit hard to make. I ended up pulling back on that idea and went to drawing board on making a collection viewer.

## Design
I am not a UI/UX expert, and honestly need to get more references to build up my abilities. However, I can use Figma. I created some components and then some layouts to better understand how the app will flow.

### Collection Card
Images are really important to NFTs. I wanted to make sure I covered all the best images I could and give the most details about the NFT Collection. I needed to provide the social links, volume, and description. The best looking images were the Collection Icon, Banner, and the First NFT. I made a nice stack of NFT image to convey that there was a collection of NFTs. Also, the banner and icon served as additional content to attach the user. Overall I think it met the objective of being informative and descriptive.

I also added an variant that was only the Collection Icon to show on various pages to provide more context. 

### NFT Card
The image should speak for itself. Minimally added a rounded boarder, because honestly those are in and hip. But I kept it minimal, name and price(or best bid). 

## Implementation
Overall the implementation went decently/smoothly. I had some minor hiccups but was able to overcome them.

### Storybook
I like to use stroybook to create my basic components. This allows for me to quickly iterate and create nice pure components. It also allows, if published, for UI and UX people to give good feedback to the frontend.

### API
I like to keep my global state and related api system in a separate folder. I also like to create custom hooks to supply my data to my components. It allows me to encapsulate my selects and dispatch(although I did not use any in this project) away from my components and allows for reuse.  
### Router
I used react-router. I was thinking on using React Navigation, however, I was not sure if I wanted to learn additional packages. But I ended up learning a fair bit since react-router v6 is different from v5, haha.

## Challenges 
### API
I had a couple challenges with the api. First was quite simple but there was a CORS issue, and I could not find any documentation for me to alter the allowed origins. I ended up creating a proxy service real quick with Pipedream. I was limited to 333 requests per day, and ended up caving into the "Professional" plan. Now sadly the API calls are a bit slow due to the proxy, but it allowed me to get started and developing.

The `nfts_filtered` endpoint really only has one filter, the collection name... Meaning traversing or looking for specific NFTs details would be hard. Also, one reason I really code not implement a safe global state. As if I wanted to view the NFT details I would have to search the whole collection for one NFT. I ended up having to pass the NFT/Collection details around via React Router. Something I was not a fan of, however, it does allow the needed data for the different pages.

I kinda winged it on the data being incomplete. I noticed that some collections did not have fields. I tried to cover any moments when a value was null. But I would probably like more specifications on what makes a "complete" collection.

### twrnc
Kinda just had some high hopes for this project, however, it sadly did not have all the design magic I wanted. I probably would switch over to React Native Grids, but it did not seem like a high priority.

### Time management
Sadly I was a bit busy during creating this project. But really I did not correctly scope out all complexities. Like any project I lead I add some padding, however, for this project I assumed a bit of ease. I spent a little over the 48 hour limit, more on the ~60 hour mark. 

## Closing Notes
Overall I did enjoy the challenge of hacking this NFT collection. Looking at the actual FTX API I think a lot of my challenges could be over come. But I think I learned a ton and got to try out some nice packages. 

I would have liked to add more unit testing. One think I like to use is Storybook Snapshot for checking that there were not any regression issues in CI. But that would probably done on a team project.

Thank you for your time, and hope my code does not scare you too much. 