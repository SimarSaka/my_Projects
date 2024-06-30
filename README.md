import os
import fitz  # PyMuPDF

def extract_text_from_pdf(file_path):
    doc = fitz.open(file_path)
    full_text = []
    for page_num in range(len(doc)):
        page = doc.load_page(page_num)
        full_text.append(page.get_text())
    return '\n'.join(full_text)

def resume_contains_keywords(resume_text, keywords):
    return any(keyword.lower() in resume_text.lower() for keyword in keywords)

def get_matching_resumes(resume_folder, keywords):
    matching_resumes = []
    for resume_file in os.listdir(resume_folder):
        if resume_file.endswith('.pdf'):
            resume_path = os.path.join(resume_folder, resume_file)
            resume_text = extract_text_from_pdf(resume_path)
            if resume_contains_keywords(resume_text, keywords):
                matching_resumes.append(resume_file)
    return matching_resumes

def main():
    resume_folder = 'C:\\Users\\simar\\OneDrive\\Desktop'  # Folder containing the resumes
    keywords = ['Python', 'Data Analysis', 'DSA']  # Keywords to match

    matching_resumes = get_matching_resumes(resume_folder, keywords)
    
    if matching_resumes:
        print('Matching Resumes:')
        for resume in matching_resumes:
            print(resume)
    else:
        print('No matching resumes found.')

if __name__ == "__main__":
    main()
