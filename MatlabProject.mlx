fullFileName = 'Project.png';
fontSize = 13;
rgbImage = imread(fullFileName);
% Get the dimensions of the image.  numberOfColorBands should be = 3.
[rows, columns, numberOfColorBands] = size(rgbImage);
% Display the original color image.
subplot(2, 2, 1);
imshow(rgbImage);
axis on;
title('Original Color Image', 'FontSize', fontSize);
% Enlarge figure to full screen.
set(gcf, 'units','normalized','outerposition',[0 0 1 1]);


% Find the black outlines.
grey=im2gray(rgbImage);
Smooth=medfilt2(grey);
BW=imbinarize(Smooth);
blackOutlines=edge(BW);

% Display the image.
subplot(2, 2, 2);
imshow(blackOutlines);
title('Black Outlines', 'FontSize', fontSize);

% Fill the outline to make it solid so we don't get boundaries
% on both the inside of the shape and the outside of the shape.
binaryImage = imfill(blackOutlines, 'holes');
% Display the image.
subplot(2, 2, 3);
imshow(binaryImage);
title('Binary Image', 'FontSize', fontSize);

% bwboundaries() returns a cell array, where each cell contains the row/column coordinates for an object in the image.
% Plot the borders of all the coins on the original grayscale image using the coordinates returned by bwboundaries.
subplot(2, 2, 4);
imshow(binaryImage);
axis on;
title('Binary Image', 'FontSize', fontSize);
title('With Boundaries, from bwboundaries()', 'FontSize', fontSize);
hold on;
boundaries = bwboundaries(binaryImage);
numberOfBoundaries = size(boundaries, 1);
for k = 1 : numberOfBoundaries
	thisBoundary = boundaries{k};
	plot(thisBoundary(:,2), thisBoundary(:,1), 'r', 'LineWidth', 3);
end
hold off;

% Define object boundaries
numberOfBoundaries = size(boundaries, 1);

for i=1:numberOfBoundaries
    [row(i),col(i)]=size(boundaries{i});
end

[val1,index1]=max(row); %largest area(more pts)

[val2,index2] = max(row(row<max(row))); %second largest area

%row=sort(row,'descend')

boundary1 = boundaries{index1};
boundary2 = boundaries{index2+1};

boundary1x = boundary1(:, 2);
boundary1y = boundary1(:, 1);

boundary2x = boundary2(:, 2);
boundary2y = boundary2(:, 1);
%plot(boundary1x,boundary1y)
%plot(boundary2x,boundary2y)

x1=1;
y1=1;
x2=1;
y2=1;
overallMinDistance = inf; % Initialize.
for k = 1 : length(boundary2)
    boundary2x = boundary2(k, 2);
    boundary2y = boundary2(k, 1);	
    % For this blob, compute distances from boundaries to edge.
    allDistances = sqrt((boundary1x - boundary2x).^2 + (boundary1y - boundary2y).^2);
    % Find closest point, min distance.
    [minDistance(k), indexOfMin] = min(allDistances);
	if minDistance(k) < overallMinDistance
		x1 = boundary1x(indexOfMin);
		y1 = boundary1y(indexOfMin);
		x2 = boundary2x;
		y2 = boundary2y;
	end
end
% Find the overall min distance
minDistance = min(minDistance);
% Report to command window.
minDistance

% Draw a line between point 1 and 2
line([x1, x2], [y1, y2], 'Color', 'y', 'LineWidth', 3);
