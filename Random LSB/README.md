
1.	Read a text as secret and covert to binary then embedded , Extract the embedded text from the image USING random LSB

```
original = imread('pngtree.jpg'); % Read the original image
cover = rgb2gray(original); % Convert the original image to grayscale
[row, column] = size(cover); % Get the dimensions of the grayscale image
L = 256; % Define the maximum intensity level
stego = cover; % Initialize the stego image with the cover image

message = input('Enter the message to be hidden: ', 's'); % Prompt the user to input the message
len = strlength(message) * 8;  % Calculate the length of the message in bits
ascii = uint8(message);   % Convert the message to ASCII values

% Convert ASCII values to binary representation
binary_all = reshape(dec2bin(ascii, 8)', 1, []);

% Shuffle the indices to embed bits randomly
random_indices = randperm(row*column);

count = 1;  % Initialize count for embedding

% Embedding loop
for k = 1:numel(random_indices)
    [i, j] = ind2sub([row, column], random_indices(k)); % Convert linear index to row and column indices
    
    % For every bit in the message
    if count <= len
        % Obtain the LSB of the grey level of the pixel
        LSB = mod(cover(i, j), 2);

        % Get the next bit to embed
        bit_to_embed = binary_all(count) - '0';

        % Perform XOR operation between the bit and the LSB
        temp = bitxor(LSB, bit_to_embed);

        % Change the bit of the stego image accordingly
        stego(i, j) = cover(i, j) + temp;

        count = count + 1;
    else
        break; % If all bits are embedded, exit loop
    end
end

% Display the cover and stego images
subplot(1, 2, 1);
imshow(cover);
title('Cover Image');

subplot(1, 2, 2);
imshow(stego);
title('Stego Image');

% Decoding the message
count = 1;
message_in_bits = '';

% Decoding loop
for k = 1:numel(random_indices)
    [i, j] = ind2sub([row, column], random_indices(k)); % Convert linear index to row and column indices
    
    % For every bit in the message
    if count <= len
        % Retrieve the LSB of the intensity level of the pixel
        LSB = mod(stego(i, j), 2);

        % Append the extracted bit to the message bit sequence
        message_in_bits = [message_in_bits, num2str(LSB)];

        count = count + 1;
    else
        break; % If all bits are decoded, exit loop
    end
end

% Convert the bit sequence into the original message
original_message = char(bin2dec(reshape(message_in_bits, 8, [])'))';

% Display the original message
disp(['The original message is: ', original_message]);
```

2.Calculate the psnr for the stego image, do visual attack and histogram attack.

```
% Calculate PSNR for the stego image
psnr_value = psnr(stego, cover);
disp(['PSNR for the stego image: ', num2str(psnr_value), ' dB']);


%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
% Visual Attack: Display the cover image and the stego image side by side for visual inspection
figure;
subplot(1,2,1);
imshow(cover);
title('Cover Image');
subplot(1,2,2);
imshow(stego);
title('Stego Image');
% Histogram Attack: Display the histograms of cover and stego images for comparison
figure;
subplot(2,1,1);
imhist(cover);
title('Histogram of Cover Image');
subplot(2,1,2);
imhist(stego);
title('Histogram of Stego Image');
```
