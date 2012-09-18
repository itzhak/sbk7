For drupal 7.15:
Installing drupal and all modules:
1. drush dl drupal
2. create new database (for example rideshare7)
3. cd drupal-7.15; drush site-install standard --account-name=admin --account-pass=goongoor --db-url=mysql://root:Yahad66@localhost/rideshare7
4. download event_rideshare module manually and fix bug number 1.
5. download all other modules needed by rideshare by next command: drush dl features views date date_views flag gmap ctools location
   for now the version that used is (features (7.x-1.0), views (7.x-3.5), date (7.x-2.6), flag (7.x-2.0-beta9), gmap (7.x-2.x-dev),
   ctools (7.x-1.2), location (7.x-3.0-alpha1)) and fix bug 2.
6. enable rideshare module and all modules that this module depend on by next command: drush pm-enable verdant_share
7. after instaling configuration: 
    a. goto admin/config/regional/settings and choose default country and default timezone.
	b. goto admin/config/services/gmap and choose api key, choose center of the map, at "marker action" choose "open info wondow"
	c. goto admin/config/content/location choose default country, and select "Use a Google Map to set latitude and longitude"
	d. goto admin/config/content/location/geocoding and choose country to use maps.
	e. goto admin/structure/block and choose "Ride Share Profile Block" to "side-bar first" choose save.
	f. goto admin/people/permissions and  Review permissions: 'Submit latitude/longitude' and 'Share Ride' Create, Edit and Delete your own content
	g. goto admin/structure/types/manage/share-ride and at "locative information" and allow "location name, street location, city, country.
	   and hide ( Coordinates, Country name, Province name, Coordinate Chooser, Postal code, State/Province, Additional.
	h. goto admin/structure/views/view/verdant_module_rideshare/edit/page_2 and at Gmap settings choose "Marker handling" by term.
	k. goto admin/structure/rideshare and choose dates.


bugs:
1. can't see markers at gmap in order ot fix it at verdant_share.module replace:
$dir =  '/' . drupal_get_path('module', 'gmap'); -> $dir =  drupal_get_path('module', 'gmap');
2. bug 2 views for gmap didn't work, apply gmap-taxonomy_markers_fix-1057922-80.patch on gmap (with eclipse).