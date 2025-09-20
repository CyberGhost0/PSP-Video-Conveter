# PSP-Video-Conveter
# A small simple shell script to convert videos files to be played on PSP 1000 series
#!/bin/bash
# PSP video converter - Preserve original quality, same or smaller size

for f in *.mp4 *.avi *.mkv; do
  [ -e "$f" ] || continue
  echo "Converting $f ..."
  ffmpeg -i "$f" -c:v libx264 -crf 23 -profile:v baseline -level 3.0 -pix_fmt yuv420p \
  -vf "scale=480:272:force_original_aspect_ratio=decrease,pad=480:272:(ow-iw)/2:(oh-ih)/2" \
  -c:a aac -ac 2 -ar 44100 -b:a 128k "PSP_${f%.*}.mp4"
done

echo "✅ All done! Copy the PSP_* files to /PSP/VIDEO/"
