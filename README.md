
1. calculate the sha256 of a file: 
openssl sha -sha256 <file>

2. find all static library and insert into archieve
find . -not -name "*unittest*" -not -name "*tests*" -name "*.o" -exec ar crs ./all.a {} +
or
#copy file recursively, with old layout
rsync -avm --include='*.a' -f 'hide,! */' <src dir> <dst dir>

3. find all the C++ header file and cp to include recursively
find ./ -name *.h -exec cp --parents '{}' ./include ';'
or
find . -name "*.h" | xargs -I {} cp --parents {} ./include

4. generate video from virtual webcam at /dev/video0
ffmpeg -f x11grab -r 15 -s 1280x720 -i :0.0+0,0 -vcodec rawvideo -pix_fmt yuv420p -threads 0 -f v4l2 /dev/video0


5. capture one image 
ffmpeg -f video4linux2 -i /dev/video0 -vframes 1 test.jpg

mplayer tv:// -tv driver=v4l2:device=/dev/video0:width=640:height=480 -frames 1 -vo jpeg


6. exam static library
ar -t all.a
insert into static archieve
ar crs all.a *.o

