guard 'shell' do
  watch(/.*\.md/) do |filenames|
    filenames.each do |filename|
      system "slideshow -o slides -t deck.js --h2 #{filename}"
    end
  end
end
