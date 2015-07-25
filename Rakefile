task :build_minified do
  sh 'uglifyjs -m sort lib/WavAudioEncoder.js > lib/WavAudioEncoder.min.js'
end

task :clean do
  sh 'rm -rf lib/WavAudioEncoder.min.js'
end

task default: :build_minified

__END__

task copy_files: :build_minified do
  sh 'cp lib/* ../WebAudioRecorder.demo/src/js'
  sh 'cp lib-minified/* ../WebAudioRecorder.demo/public/js'
end

