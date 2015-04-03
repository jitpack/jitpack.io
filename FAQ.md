Frequently Asked Questions
-

**Can version ranges be used with JitPack?**

Not at the moment. 


**What happens if a tag is deleted on GitHub?**

If the project was already built JitPack will continue serving the existing artifacts. It will not rebuilt the project at the new tag. 
In case you need to redo a release the best option is to create a new patch version.

