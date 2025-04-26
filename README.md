# import os
import shutil

# Define the folder to organize (replace with your folder path)
source_folder = "C:/Users/Kelvin/Downloads"  # Example: Update this to your folder
file_types = {
    "Images": [".jpg", ".png", ".gif"],
    "Documents": [".pdf", ".docx", ".txt"],
    "Videos": [".mp4", ".mkv"],
    "Others": []
}

# Create destination folders
for folder in file_types.keys():
    folder_path = os.path.join(source_folder, folder)
    try:
        if not os.path.exists(folder_path):
            os.makedirs(folder_path)
    except Exception as e:
        print(f"Error creating folder {folder}: {e}")

# Organize files
for filename in os.listdir(source_folder):
    file_path = os.path.join(source_folder, filename)
    if os.path.isfile(file_path):
        file_ext = os.path.splitext(filename)[1].lower()
        moved = False
        for folder, extensions in file_types.items():
            if file_ext in extensions:
                try:
                    shutil.move(file_path, os.path.join(source_folder, folder, filename))
                    print(f"Moved {filename} to {folder}")
                    moved = True
                    break
                except Exception as e:
                    print(f"Error moving {filename}: {e}")
        if not moved and file_ext:
            try:
                shutil.move(file_path, os.path.join(source_folder, "Others", filename))
                print(f"Moved {filename} to Others")
            except Exception as e:
                print(f"Error moving {filename}: {e}")

print("File organization complete!")
