# tl;dr

This module provides a collection of clean-up tools for your silverstripe website.

The way you use it is that you install it as a dev requirement and then run a bash script like this:

## USE AT YOUR OWN RISK

Simply get an sspak from your live site and run it locally, then, super carefully, consider what is missing!

## Example Usage

The example provided here is just one way to do it.  There are many ways to use this module.

Please review all tasks used here and also look at the other modules included, not used below.

```shell
#!/bin/bash

##### ##### ##### ##### 
# install with dev requirements!
##### ##### ##### ##### 

composer install --dev sunnysideup/spring-clean-recipe:dev-main
composer install 

##### ##### ##### ##### 
# clean up the database structures
##### ##### ##### #####

vendor/bin/sake dev/build flush=all
vendor/bin/sake dev/tasks/dataintegritytest do=obsoletefields deleteall=1
vendor/bin/sake dev/tasks/dataintegritytest do=deleteobsoletetables
vendor/bin/sake dev/tasks/dataintegritytest do=tablereview makeobsolete=1 deletetablealltogether=1

# with the next dev/build you want to carefully check for any fields / tables being (re)created
# this means you have been a bit too ruthless ;-)
vendor/bin/sake dev/build flush=all

##### ##### ##### ##### 
# clean up files
##### ##### ##### ##### 

vendor/bin/sake dev/tasks/UnusedFileReportBuildTask
vendor/bin/sake dev/tasks/delete-all-unused-files
vendor/bin/sake dev/tasks/delete-files-from-disk-not-found-in-database

##### ##### ##### ##### 
# resize your remaining images
##### ##### ##### ##### 
vendor/bin/sake dev/tasks/resize-all-images --for-real=1
vendor/bin/sake dev/tasks/fix-hashes --for-real=1

##### ##### ##### ##### 
# delete stale data
##### ##### ##### ##### 

# here we are deleting ALL versioned data, you can of course do that more thoughtfully
# using some of the modules provided with this recipe

vendor/bin/sake dev/tasks/Sunnysideup-DeleteAllTables-DeleteAllVersionedData
vendor/bin/sake dev/build flush=all

##### ##### ##### ##### 
# Elemental cleanup
##### ##### ##### ##### 

# if you use Elemental, then run the below to remove orphaned records:

vendor/bin/sake dev/tasks/remove-orphaned-elements confirm=1
vendor/bin/sake dev/build flush=all


##### ##### ##### ##### 
# remove dev requirements
##### ##### ##### ##### 

composer install --no-dev
vendor/bin/sake dev/build flush=all


